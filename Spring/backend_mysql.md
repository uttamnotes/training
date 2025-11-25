# Simplest workflow — connect React → Spring Boot → MySQL (quick, copy-pasteable)

Below is a compact, practical workflow you can follow start-to-finish. I’ll give the exact commands, the smallest Java code snippets you need, the React side (using `create-react-app`), how to solve CORS during development, and how to serve the React build from Spring Boot for production.

---

## 1) Prereqs

* Java 17+ (or 11) and Maven (or Gradle).
* Node 16+ and npm/yarn.
* MySQL server running (or use Docker).
  (These are standard requirements; Spring’s MySQL guide is a good reference.) ([Home][1])

---

## 2) Create the Spring Boot backend

Use Spring Initializr (or `start.spring.io`) with dependencies:

* **Spring Web**
* **Spring Data JPA**
* **MySQL Driver**
* (optional) Spring Security / Lombok if needed

Example: generate project or use Maven:

```bash
# if using curl to start a project (example)
# or just use start.spring.io UI
```

**Add MySQL Connector (Maven)**

```xml
<dependency>
  <groupId>mysql</groupId>
  <artifactId>mysql-connector-j</artifactId>
</dependency>
```

**application.properties** (minimal):

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb?useSSL=false&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update   # use update for dev; none for prod
spring.jpa.show-sql=true
```

(Use Spring Data JPA + MySQL as shown in the Spring guide.) ([Home][1])

**Simple JPA entity + repo + REST controller**

`User.java`

```java
@Entity
public class User {
  @Id @GeneratedValue
  private Long id;
  private String name;
  private String email;
  // getters/setters or Lombok
}
```

`UserRepository.java`

```java
public interface UserRepository extends JpaRepository<User, Long> {}
```

`UserController.java` — allow CORS for local dev:

```java
@RestController
@RequestMapping("/api/users")
@CrossOrigin(origins = "http://localhost:3000")   // allow React dev server
public class UserController {
  private final UserRepository repo;
  public UserController(UserRepository repo){ this.repo = repo; }

  @GetMapping
  public List<User> all(){ return repo.findAll(); }

  @PostMapping
  public User create(@RequestBody User u){ return repo.save(u); }
}
```

For a global approach to CORS see Spring’s CORS guide. ([Home][2])

---

## 3) Start MySQL (quick)

Either locally:

```sql
CREATE DATABASE mydb;
CREATE USER 'app'@'localhost' IDENTIFIED BY 'pw';
GRANT ALL ON mydb.* TO 'app'@'localhost';
```

Or with Docker:

```bash
docker run --name mysql-dev -e MYSQL_ROOT_PASSWORD=pass -e MYSQL_DATABASE=mydb -p 3306:3306 -d mysql:8
```

---

## 4) Run the Spring Boot backend

```bash
# from backend project folder
mvn spring-boot:run
# or build and run jar
mvn package
java -jar target/myapp-0.0.1-SNAPSHOT.jar
```

Verify `http://localhost:8080/api/users` returns `[]` (or JSON).

Resources and full examples for CRUD with Spring Boot + MySQL are widely available (examples/tutorials). ([BezKoder][3])

---

## 5) Create the React frontend

From another folder:

```bash
npx create-react-app react-frontend
cd react-frontend
npm install axios
```

**Simple Axios example to call backend**
`src/App.js`

```js
import React, {useEffect, useState} from 'react';
import axios from 'axios';

function App(){
  const [users, setUsers] = useState([]);
  useEffect(()=>{
    axios.get('/api/users')   // see dev proxy below
      .then(r=>setUsers(r.data))
      .catch(e=>console.error(e));
  },[]);
  return (
    <div>
      <h1>Users</h1>
      <ul>{users.map(u => <li key={u.id}>{u.name} ({u.email})</li>)}</ul>
    </div>
  );
}
export default App;
```

### Option A — Development: avoid CORS with `proxy` (quick)

Add in `react-frontend/package.json`:

```json
"proxy": "http://localhost:8080"
```

Then `axios.get('/api/users')` will forward to `http://localhost:8080/api/users` during `npm start`. This is simple for local dev.

### Option B — Or keep full URLs and enable CORS on backend

If you use full URL `http://localhost:8080/api/users`, the backend must allow cross origin (see `@CrossOrigin` earlier). See Spring CORS guide. ([Home][2])

Run React dev server:

```bash
npm start
# opens http://localhost:3000
```

(Using `proxy` removes need to configure CORS during dev.)

---

## 6) Production: serve React from Spring Boot (optional, simple)

Build React and copy into Spring Boot `resources/static`, or configure Maven/Gradle to do it automatically.

From React:

```bash
npm run build
# copy build/* into backend/src/main/resources/static (or configure CI)
```

Spring Boot will then serve React at `/` and REST APIs remain under `/api/*`. OKTA tutorial shows packaging React inside Spring Boot for production workflows. ([Okta Developer][4])

---

## 7) Extra: security, connection pool, and best practices

* Spring Boot uses HikariCP by default; tune pool size in `application.properties` for production. ([Medium][5])
* Don’t keep DB creds in properties in production — use environment variables or secrets manager.
* For CORS in production prefer same-origin (use reverse proxy/nginx) rather than enabling wide CORS. Using nginx reverse proxy can simplify CORS and SSL. ([Medium][6])

---

## 8) Minimal checklist you can follow right now

1. Create Spring Boot project with Web, JPA, MySQL driver.
2. Configure `application.properties` for MySQL and create the DB.
3. Add entity, repository, controller (`@CrossOrigin` for dev).
4. `mvn spring-boot:run` — verify API works with Postman.
5. Create React app, install axios. Add `proxy` to `package.json` or call full backend URL.
6. `npm start` — open React, confirm it loads data from `/api/...`.
7. For prod: `npm run build` → place files in `backend/src/main/resources/static` and run the Spring Boot jar.

---

## Helpful links / example tutorials (to read or clone)

* Spring guide: Accessing data with MySQL. ([Home][1])
* Fullstack React + Spring Boot CRUD tutorial (Bezkoder). ([BezKoder][3])
* Okta tutorial showing packaging React into Spring Boot (good for prod packaging). ([Okta Developer][4])
* CORS handling in Spring Boot — official guide & community articles. ([Home][2])

---

If you want, I can:

* Generate a **starter repo** structure (file list + exact code files) for both backend and frontend that you can copy-paste, or
* Give you a **Docker Compose** file to run MySQL + backend + React dev server together.

Which of those would you like me to produce right away? (I can paste the full files inline.)

[1]: https://spring.io/guides/gs/accessing-data-mysql?utm_source=chatgpt.com "Getting Started | Accessing data with MySQL - Spring"
[2]: https://spring.io/guides/gs/rest-service-cors?utm_source=chatgpt.com "Enabling Cross Origin Requests for a RESTful Web Service"
[3]: https://www.bezkoder.com/react-spring-boot-crud/?utm_source=chatgpt.com "Spring Boot + React + MySQL: CRUD example REST APIs"
[4]: https://developer.okta.com/blog/2022/06/17/simple-crud-react-and-spring-boot?utm_source=chatgpt.com "Use React and Spring Boot to Build a Simple CRUD App"
[5]: https://medium.com/%40AlexanderObregon/connecting-spring-boot-applications-to-mysql-databases-ea025e4b5f19?utm_source=chatgpt.com "Connecting Spring Boot Applications to MySQL Databases"
[6]: https://medium.com/%40sridhar.jammalamadaka/solving-cors-challenges-in-a-spring-boot-react-setup-with-nginx-e9ab50137260?utm_source=chatgpt.com "Solving CORS Challenges in a Spring Boot & React Setup ..."
