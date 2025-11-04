# Basic Typeorm Concepts 
___
## Setting up the Development Environment
___

Initialize a Node.js Project

 ### Create a Project Directory:
```js
mkdir my-node-project
cd my-node-project

```

### Initialize the Project:
```js
npm init -y
```
This will create a package.json file which manages project dependencies and configuration.

### Install Project Dependencies:
Install Typescript and Node.js types:
```js
npm install typescript ts-node @types/node --save-dev
```
`typescript:` The Typescript Compiler  
`ts-node:` a Node.js library to run Typescript code without needing to compile it manually.  
`@types/node:` Type definitions for Node.js, providing type support in Typescript.

### Install Typeorm and Database Driver:
If you're using a database like Postgresql, install pg as the driver:
```js
npm install typeorm reflect-metadata pg
```
`typeorm:` The ORM library  
`reflect-metadata:` Required By typeorm for Typescript decorators.  
`pg:` Postgresql Driver. (For other databases, use the appropriate driver, like mysql2 for MySql.)

### Create a tsconfig.json file:
This file configures the typescript compiler options. Generate a basic tsconfig.json by running:
```js
tsc --init
```
Open tsconfig.json and modify some settings for a typical Node.js project:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules"]
}
```
`Key Options:`  
"experimentalDecorators" and "emitDecoratorMetadata" are required by typeorm for using decorators.
"rootDir" points to the directory where Typescript files are stored, typically src.
"outDir" is the output directory for compiled javascript files, usually dist.

### Configure Typeorm:
create a ormconfig.json file in the project root to define the database connection.

#### Example ormconfig.json:

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "your_username",
  "password": "your_password",
  "database": "your_database",
  "entities": [
    "src/entity/**/*.ts"
  ],
  "migrations": ["src/migration/**/*.ts"],
  "cli": {
    "entitiesDir": "src/entity",
    "migrationsDir": "src/migration"
  }
}
```

## Folder Structure for this Typeorm Configuration using Nodejs
___
Explaination of Each Folder and File:  
`src/entity:` Contains Typeorm entity files, each representing a table in the database. For instance,  User.ts defines the User entity.
`src/migrations:` Stores migration files for managing database schema changes.  
`src/controllers:` Holds controller files responsible for handling HTTP requests.  
`src/service:` contains business logic (services) that interact with the repositories or external systems.  
`src/config:` Configuration files, such as database connection setup.  
`src/routes:` Defines all API endpoints. Each file typically represents routes for a specific entity or feature.  
`src/app.ts`: sets up the main application, including middleware and routing.
`src/index.ts`: The entrypoint , where the server is started.

### Sample Commands:
To start the server in development mode, add these scripts in the package.json:

```json
"scripts":{
"start":"node dist/index.js",
"build":"tsc",
"dev":"ts-node-dev src/index.ts"
}
```
`npm run build:` Compiles Typescript to Javascript  
`npm start:` Runs the compiled code from the dist directory.  
`npm run dev:` Runs the server with ts-node-dev for automatic restarts on code changes (install ts-node-dev as a dev dependency).

This setup provides a solid foundation for a Node.js application with Typescript and Typeorm,   
ensuring an organized structure that can be easily expanded as the project grows.

## How to connect Typeorm to Mysql/Postgresql in Node.js and Typescript
___
Setting up Typeorm and Database Connection

- Installing Typeorm and necessary dependencies 
- Configuring Typeorm with Postgresql/MySql
- Setting up environment variables for database connection

Here's a guide on setting up the Typeorm with a Postgresql or MySql database connection in your Node.js application,  including installing dependencies, configuring Typeorm, and managing environment variables for sensitive data.

### Setting up Typeorm and database connection
1. Installing Typeorm and Necessary Dependencies
To use Typeorm in your project, you'll need to install the ORM library along with the appropriate database driverbased on your chosen database. Here's how to do it (on both Postgresql and Mysql:)  
`For Postgresql:`
        Open your terminal and navigate to your project directory.
        Install Typeorm and the Postgresql server

```js
npm install typeorm reflect-metadata pg
```

`For MySql:` Open your terminal and navigate to your project directory.
Install Typeorm and Mysql driver:
```js
npm install typeorm reflect-metadata mysql2
```
2. Configuring Typeorm with Postgresql/MySql
After installing the necessary dependencies, you need to configure typeorm to connect to your database.  
 `Option A:` using ormconfig.json (recommended for simple setup)
   Create a ormconfig.json file in the root of your project if you haven't already done so. here's how to configure it for both databases:

### Postgresql Configuration:
```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "your_username",
  "password": "your_password",
  "database": "your_database",
  "synchronize": true, // set to false in production
  "logging": true,
  "entities": [
    "src/entity/**/*.ts"
  ],
  "migrations": ["src/migration/**/*.ts"],
  "cli": {
    "entitiesDir": "src/entity",
    "migrationsDir": "src/migration"
  }
}
```
### MySql Configuration:
```json
{
  "type": "mysql",
  "host": "localhost",
  "port": 5432,
  "username": "your_username",
  "password": "your_password",
  "database": "your_database",
  "synchronize": true, // set to false in production
  "logging": true,
  "entities": [
    "src/entity/**/*.ts"
  ],
  "migrations": ["src/migration/**/*.ts"],
  "cli": {
    "entitiesDir": "src/entity",
    "migrationsDir": "src/migration"
  }
}
```
`Option B:` Using a Datasource in Typescript (recommended for more control or big projects)  
You can also configure Typeorm directly  in your Typescript code. This method is more flexible and allows you to use environment variables for sensitive information.

Create a New file named data-source.ts in the src directory:
```ts
import {DataSource} from "typeorm";
import {User} from "./entity/user";

const AppDataSource=new DataSource({
   type:"postgres",
   host:process.env.DB_HOST,
   port:Number(process.env.DB_PORT),
   username:process.env.DB_USERNAME,
   password:process.env.DB_PASSWORD,
   database:process.env.DB_NAME,
   synchronize:true,
   logging:true,
   entities:[User],
   migrations:[] 
});

export default AppDataSource;
```

Integrate it into your main entry point  (index.ts or app.ts)

```ts
import "reflect-metadata";  //import reflect-metadata at the top
import AppDataSource from "./data-source";

const startApp=async ()=>{
    await AppDataSource.initialize().then(()=>{
        console.log("Data Source has been initialized!");
    }).catch((error)=>{
        console.error("Error during Data Source initialization, error");
    })
};

startApp();

```

3. Setting up Environment variables for Database Connection
To manage sensitive information (like database credentials) safely, it;s best to use environment varibales. Here's how to set these up:

`Install Dotenv:` This package loads environment varibales from a .env file into a process.env.

```js
npm install dotenv
```

Create a .env file : In the root of your project, create a .env file:

```js
DB_HOST= localhost
DB_PORT= 5432    //Use 3306 for MYSQL
DB_USERNAME=your_username
DB_PASSWORD=your_password
DB_NAME=your_database
```

Load the environment variables: At the begining of your data-source.ts, load the dotenv package:

```ts
import {config} from "dotenv";
config();

const AppDataSource=new DataSource({
    type:"postgres",
    host:process.env.DB_HOST,
    port:Number(process.env.DB_PORT),
    username:process.env.DB_USERNAME,
    password:process.env.DB_PASSWORD,
    database:process.env.DB_NAME,
    synchronize:true,
    logging:true,
    entities:[User],
    migrations:[]
});
```

`Summary:`  
By Following these steps, you've setup typeorm with the Postgresql or MySql database connection, configured it to work with your Typescript application, and managed sensitive database credentials using environment variables. This setup will help you create a solid foundation for your application's data layer.

## How to Define Models And Entities in Typeorm
___
- What are Entities and how to define them in Typeorm
- Creating basic Entities with Typescript
- Understanding Typeorm Decorators

### 1. What are Entities and how to define them in Typeorm  
Entities in Typeorm are classes that map to database tables. Each entity class contains properties that represent the column of the table. By defining entities, you can interact with the database using Javascript/typescript objects rather than raw sql queries, making your code cleaner and easier to maintain.

Basic structure of an entity:
- Each entity class must be decorated with @Entity.
- Each property within the class can be decorated with various decorators to define its characterstics.  

### 2. Creating Basic Entities with Typescript
Create a Entity file: Inside the src/entity directory create a file named User.ts.

`Define the Entity: `  
```ts
import {Entity, PrimaryGeneratedColumn, Column} from 'typeorm';

@Entity() // Decorator to indicate that this class is an entity.
export class User{
    @PrimaryGeneratedColumn() //Primary key Column , auto-increment
    id:number;
    
    @Column() //Regular Column
    firstName:string;

    @Column() //Regular Column
   lastName:string;

    @Column() //Regular Column
    email:string;

    @Column({default:true}) //Column with a default value
    isActive:boolean;
    
}
```

`Explaination of the User Entity:`  
- @Entity(): Marks the class as an Entity that maps to a database table. The table name will default to the class name (user), but it can be customized by passing a string argument, e.g. @Entity('users').  
- @PrimaryGeneratedColumn(): Defines the primary key column that auto-increments. You can use @PrimaryColumn() for non-generated keys.  
- @Column(): Represents a regular column in the table. Additional Options can be provided to customize behaviour (e.g. data types, constraints).  
- {default:true}: This options sets a default value for the column.

### 3. Understanding TypeOrm Decorators
Typeorm provides various decorators to define entity properties  and relationships effectively. Here are some commonly used decorators:  
- @Entity(name?:string): Marks a class as an Entity. The Optional name parameter defines the table name.  
- @PrimaryGeneratedColumn(): Used for primary keys that auto-increments. You can use @PrimaryColumn() for non-generated keys.
- @Column(options?:ColumnOptions): Defines a column in the Table. The options parameter can specify:  
type: Data type (e.g. String, Number, Boolean, etc.)  
length: length for string types.  
nullable: Whether the column can be null.  
default: Default value for the column.

- @ManyToOne(): Defines a many-to-one relationship with another entity.
- @OneToMany(): Defines a One-to-many relationship with another entity.
- @ManyToMany(): Defines a many-to-many relationship between two entities.
- @OneToOne(): Defines a one-to-one relationship with another entity.
- @JoinColumn(): Specifies the column that joins two entities in a relationship.

### Example of a Relationship:
Here's a quick example of how you might define relationships  using Typeorm decorators:

```ts
import {Entity, PrimaryGeneratedColumn, Column, OneToMany} from "typeorm";
import {Post} from "./Post"; // Assuming a Post Entity Exist

@Entity()
export class User{
    @PrimaryGeneratedColumn()
    id:number;
    
    @Column()
    name:string;
    
    @OneToMany(()=>Post,post => post.user)  // One User can have many posts
    posts:Post[];
}
```
And the corresponding Post entity might look like this:

```ts
import {Entity, PrimaryGeneratedColumn, Column, ManyToOne} from "typeorm";
import  {User} from "./User";

@Entity()
export class Post{
    @PrimaryGeneratedColumn()
    id:number;
    
    @Column()
    title:string;
    
    @ManyToOne(()=>User,user=>user.posts) //Many posts belongs to one user
    user:User
    
}
```
          


