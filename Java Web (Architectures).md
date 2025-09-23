### Tier vs Layer
**Tier**: physical separation (runs on a separate machine or server)
**Layer**: logical separation inside code (a module or package with a responsibility)

**Example**:
Presentation layer -> Controllers, RestControllers
Business layer -> Services
Data layer -> Repositories, Entities

### 1-Tier (Mainframe architecture): 
- All programs and data is stored on one central machine

### 2-tier (Client-Server architecture): 
- Client machine run an application, it talks to the server
- Server usually runs DBMS (Database management system)

**Client application**
- Presentation logic (interface)
- Navigation (users move between screens)
- Business rules (logic that defines how system behaves)
- Database access code (queries sent directly to the server)

**Server**:
- Storing and managing data
- Handling requests from clients
- Returning requests results

**Problem**: If business rules changed had to be updated on every user's PC

### 3-Tier (N-Tier)
Separates system into three main tiers:
- **Presentation Tier (Client):** browser, mobile app or desktop app 
	 **Techs**: React, Angular
- **Business Logic / Application Tier (Middle layer):** application server 
	 **Techs**: Spring Boot, Node.js
- **Data Tier (Database server)**
	 **Techs**: MySQL, PostgreSQL

Benefits of this architecture:
- Flexibility
- Maintainability
- Reusability
- Scalability
- Reliability
- Security
- Load Balancing

![[java_web_arch_3tier.png]]

**What goes in each layer (3 layer pattern)**
**Presentation**:
- Controllers, Request/Responses DTOs, Input validation, Exception handling
**Business**:
- Service classes, Service implementations, Transaction management, Mappers, Service interfaces
**Data**:
- Repository interfaces, Entity classes, Database operations, Data Access Objects (DAOs) (legacy)

