# Setting up Typeorm Connection With ormconfig.json
___

```js
npm install typeorm reflect-metadata pg dotenv  
npm install --save-dev typescript ts-node @types/node
```

Create a ormconfig.json file for writing the credentials:
```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "your_username",
  "password": "your_password",
  "database": "your_database",
  "synchronize": true,
  "logging": false,
  "entities": ["src/entity/**/*.ts"],
  "migrations": ["src/migration/**/*.ts"],
  "cli": {
    "entitiesDir": "src/entity",
    "migrationsDir": "src/migration"
  }
}
```

Create a User entity in src/entity/User.ts:
```ts
import {Entity, PrimaryGeneratedColumn, Column} from 'typeorm';

@Entity()
export class User{
    @PrimaryGeneratedColumn()
    id:number;
    
    @Column
    firstName:string;
    
    @Column()
    lastName:string;
    
    @Column()
    email:string
    
    @Column({default:true})
    isActive:boolean;
}
```

Make this code into main file called index.ts 
```ts
import 'reflect-metadata';
import {createConnection} from 'typeorm';
import {User} from "./entity/User";

async function main(){
    try{
    //     initialize the database connection using ormconfig.json 
        const connection=await createConnection();
        console.log("Database Connected Successfully.");
        
    //     Get the Repository for the User entity
        const userRepository=connection.getRespository(User);
        
    //     Create and save a new User instance
        const newUser=userRepository.create({
            firstname:'Jane',
            lastname:'Doe',
            email:'jane.doe@example.com',
            isActive:true
        });
        
        await userRespository.save(newUser);
        console.log("New User Saved: ",newUser);
        
    //     Optional: close the connection if not using connection pooling
        await connection.close();
        
        
    }catch(error){
        console.log("error during database connection initialization",error);
    }
}

// Run the main function to initialize the app
main();
```
Add these scripts into the package.json file:

```json
{
  "scripts": {
    "start": "node dist/index.ts",
    "build": "tsc",
    "dev": "ts-node src/index.ts"
  }
}
```



