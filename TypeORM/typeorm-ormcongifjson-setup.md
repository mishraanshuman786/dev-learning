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

