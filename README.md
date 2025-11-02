# 🏦 National Bank Application

<div align="center">

![Java](https://img.shields.io/badge/Java-17-orange.svg)
![Jakarta EE](https://img.shields.io/badge/Jakarta%20EE-10.0-blue.svg)
![Maven](https://img.shields.io/badge/Maven-3.6+-red.svg)

**A comprehensive, enterprise-grade banking system built with Jakarta EE, featuring role-based access control, automated transactions, and real-time notifications.**

[Features](#-features) • [Technologies](#-technologies) • [Getting Started](#-getting-started) • [Architecture](#-architecture) • [Screenshots](#-screenshots)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Technologies](#-technologies)
- [Architecture](#-architecture)
- [Getting Started](#-getting-started)
- [Configuration](#-configuration)
- [API Documentation](#-api-documentation)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

**National Bank Application** is a modular, enterprise-level banking system designed to demonstrate modern Jakarta EE (formerly Java EE) concepts. This application provides a secure, scalable solution for banking operations with robust transaction management, automated scheduling, and comprehensive audit trails.

### Key Highlights

✨ **Modular Architecture** - Built with Maven multi-module structure for maintainability  
🔒 **Enterprise Security** - Role-based access control with Jakarta Security API  
⏱️ **Automated Tasks** - EJB Timer Service for scheduled transfers and interest calculations  
📧 **Real-time Notifications** - JavaMail integration for OTP, confirmations, and alerts  
📊 **Performance Monitoring** - Custom interceptors for audit logging and performance tracking  
💳 **Transaction Management** - Robust error handling and transaction rollback support

---

## ✨ Features

### 🔐 Authentication & Authorization

- **Multi-role Access Control**
  - Customer portal for account management
  - Employee dashboard for customer services
  - Admin panel for system administration
- **Secure Login System** with session management
- **Password Encryption** using industry-standard algorithms
- **Email Verification** for new registrations

### 💰 Account Management

- **Account Creation** with automatic account number generation
- **Multiple Account Types** (Savings, Checking, etc.)
- **Account Balance Tracking** with real-time updates
- **Transaction History** with detailed logs
- **Account Status Management** (Active, Suspended, Closed)

### 💸 Fund Transfers

- **Secure Transfers** with OTP (One-Time Password) verification
- **Real-time Transfer Processing** with immediate balance updates
- **Transfer History Tracking** with comprehensive audit logs
- **Transfer Status Monitoring** (Pending, Completed, Failed)

### 📅 Scheduled Transactions

- **Automated Fund Transfers** using EJB Timer Service
- **Recurring Payment Support** with flexible scheduling
- **Error Notification System** for failed scheduled transfers
- **Transaction History** for all scheduled operations

### 📊 Monitoring & Logging

- **Performance Interceptors** - Track method execution time
- **Audit Interceptors** - Comprehensive activity logging
- **Exception Handling** - Centralized error management
- **Transaction Rollback** - Automatic rollback on failures

### 📧 Email Notifications

- **OTP Delivery** for fund transfer verification
- **Registration Confirmations** for new customers/employees
- **Scheduled Transfer Alerts** for failures and completions
- **System Notifications** for important account events

### 💡 Interest Calculation

- **Automated Interest Processing** via EJB Timer Service
- **Periodic Calculation** of interest on eligible accounts
- **Background Processing** without user intervention

---

## 🛠️ Technologies

### Backend

| Technology | Version | Purpose |
|------------|---------|---------|
| **Java** | 17 | Core programming language |
| **Jakarta EE** | 10.0 | Enterprise Java platform |
| **EJB** | 4.0 | Business logic & session beans |
| **JPA** | 3.1 | Persistence layer |
| **Jakarta Security** | 3.0 | Authentication & authorization |
| **EJB Timer Service** | - | Scheduled task execution |
| **JavaMail API** | 2.1 | Email notifications |
| **JMS** | 3.1 | Messaging services |

### Frontend

| Technology | Purpose |
|------------|---------|
| **JSP** | Server-side rendering |
| **JSTL** | Template tags |
| **JavaScript** | Client-side interactivity |
| **CSS** | Styling |

### Build & Tools

| Tool | Purpose |
|------|---------|
| **Maven** | Dependency management & build |
| **Payara Server** | Jakarta EE application server |
| **IntelliJ IDEA** | IDE |

### Dependencies

- **Jakarta Jakarta EE API** (10.0.0) - Core enterprise APIs
- **Gson** (2.13.1) - JSON processing
- **Jakarta Servlet JSP JSTL** (3.0.1) - JSP and JSTL support

---

## 🏗️ Architecture

### Modular Structure

```
bank-application-bcd2/
│
├── 📦 core-module/           # Core Business Logic
│   ├── dto/                  # Data Transfer Objects
│   ├── model/                # Entity classes (JPA)
│   ├── enums/                # Enumerations
│   ├── service/              # Service interfaces
│   ├── mail/                 # Email templates & services
│   ├── util/                 # Utility classes
│   ├── annotation/           # Custom annotations
│   └── exception/            # Custom exceptions
│
├── 📦 ejb-module/            # Enterprise JavaBeans
│   ├── beans/                # Session beans (Stateless, Singleton)
│   │   ├── AccountSessionBean
│   │   ├── CustomerSessionBean
│   │   ├── TransferSessionBean
│   │   ├── ScheduleTransferSessionBean
│   │   └── UserSessionBean
│   ├── interceptors/         # Cross-cutting concerns
│   │   ├── AuditInterceptor
│   │   └── PerformanceInterceptor
│   └── timers/               # Scheduled tasks
│       ├── ScheduledFundTransferBean
│       └── InterestCalculatorBean
│
├── 📦 web-module/            # Web Layer
│   ├── action/               # Servlet controllers
│   │   ├── Login, Register, LogOut
│   │   ├── FundTransfer, VerifyTransfer
│   │   ├── ScheduleFundTransfer
│   │   └── AddCustomer, AddEmployee
│   ├── security/             # Security implementation
│   │   ├── AppIdentityStore
│   │   └── AuthMechanism
│   └── webapp/               # Web resources
│       ├── JSP pages
│       ├── CSS/JS
│       └── WEB-INF/
│
└── 📦 ear-module/            # Enterprise Archive
    └── META-INF/
        └── application.xml   # Deployment descriptor
```

### Design Patterns

- **Session Facade** - EJB session beans provide business logic abstraction
- **DAO Pattern** - Data access through JPA repositories
- **Interceptor Pattern** - Cross-cutting concerns (audit, performance)
- **Service Layer** - Business logic separation
- **DTO Pattern** - Data transfer between layers

### Security Architecture

```
┌─────────────────┐
│   JSP Pages      │
└────────┬────────┘
         │
┌────────▼────────┐
│  Servlet Layer  │
└────────┬────────┘
         │
┌────────▼────────┐
│  Security API   │ ◄─── Role-based access control
│  (Identity Store│
│   & Auth)       │
└────────┬────────┘
         │
┌────────▼────────┐
│  EJB Session    │ ◄─── Business Logic
│     Beans       │
└────────┬────────┘
         │
┌────────▼────────┐
│   JPA Entities  │ ◄─── Data Persistence
│   & Database    │
└─────────────────┘
```

---

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- ☕ **Java JDK 17+** - [Download](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
- 📦 **Maven 3.6+** - [Download](https://maven.apache.org/download.cgi)
- 🐠 **Payara Server 6+** (or any Jakarta EE 10 compatible server) - [Download](https://www.payara.fish/downloads/)
- 🔧 **IDE** (Optional but recommended) - IntelliJ IDEA, Eclipse, or VS Code

### Installation Steps

#### 1. Clone the Repository

```bash
git clone https://github.com/DisuraAberathna/national-bank.git
cd national-bank
```

#### 2. Build the Project

```bash
# Clean and build all modules
mvn clean install

# This will:
# - Compile all modules
# - Run tests (if any)
# - Package JAR, WAR, and EAR files
# - Generate artifacts in target/ directories
```

#### 3. Deploy to Payara Server

**Option A: Using Payara Admin Console**

1. Start Payara Server:
   ```bash
   # Navigate to Payara bin directory
   cd <PAYARA_HOME>/bin
   
   # Start server (Windows)
   asadmin start-domain domain1
   
   # Start server (Linux/Mac)
   ./asadmin start-domain domain1
   ```

2. Access Admin Console:
   - Open browser: `http://localhost:4848`
   - Default credentials: `admin` / `admin`

3. Deploy EAR file:
   - Go to **Applications** → **Deploy**
   - Select: `ear-module/target/bank-app-ear.ear`
   - Click **OK**

**Option B: Using Command Line**

```bash
# Deploy via asadmin command
asadmin deploy ear-module/target/bank-app-ear.ear

# Or with specific context root
asadmin deploy --contextroot bank-web ear-module/target/bank-app-ear.ear
```

**Option C: Hot Deployment**

Simply copy the EAR file to Payara's autodeploy directory:

```bash
cp ear-module/target/bank-app-ear.ear <PAYARA_HOME>/glassfish/domains/domain1/autodeploy/
```

#### 4. Access the Application

Once deployed, access the application at:

```
http://localhost:8080/bank-app-frontend/
```

### Default Access

After deployment, you can register new users or use default credentials (if configured in database seeding).

---

## ⚙️ Configuration

### Database Configuration

Configure your database connection in `persistence.xml` (typically in `core-module/src/main/resources/META-INF/`):

```xml
<persistence-unit name="BankPU" transaction-type="JTA">
    <jta-data-source>jdbc/bankDB</jta-data-source>
    <!-- Add your persistence classes -->
</persistence-unit>
```

**Setup Data Source in Payara:**

1. Go to **Resources** → **JDBC** → **JDBC Connection Pools**
2. Create a new connection pool
3. Configure with your database details
4. Create a JDBC resource named `jdbc/bankDB`

### Email Configuration

Update `core-module/src/main/resources/application.properties`:

```properties
mailtrap.host = sandbox.smtp.mailtrap.io
mailtrap.port = 2525
mailtrap.username = YOUR_USERNAME
mailtrap.password = YOUR_PASSWORD
mailtrap.email = bank@bank-app.com
app.path = http://localhost:8080/bank-app
```

**For Production:**

- Use a production SMTP server (Gmail, SendGrid, AWS SES, etc.)
- Update host, port, and credentials accordingly
- Enable SSL/TLS for secure connections

### Application Context

Update the application path in `application.properties` if deploying to a different context root:

```properties
app.path = http://localhost:8080/YOUR_CONTEXT_ROOT
```

---

## 📚 API Documentation

### Session Beans

#### AccountSessionBean

```java
@Stateless
public class AccountSessionBean {
    // Account CRUD operations
    Account createAccount(AccountDTO dto);
    Account updateAccount(AccountDTO dto);
    Account findByAccountNumber(String accountNumber);
    List<Account> findByCustomerId(Long customerId);
}
```

#### TransferSessionBean

```java
@Stateless
public class TransferSessionBean {
    // Transfer operations
    TransferHistory initiateTransfer(TransferHistoryDTO dto);
    TransferHistory verifyTransfer(String otp, Long transferId);
    TransferHistory validateTransfer(Long transferId);
    List<TransferHistory> getTransferHistory(Long accountId);
}
```

#### ScheduleTransferSessionBean

```java
@Stateless
public class ScheduleTransferSessionBean {
    // Scheduled transfer operations
    ScheduledTransfer scheduleTransfer(ScheduledTransferDTO dto);
    void cancelScheduledTransfer(Long scheduledTransferId);
    List<ScheduledTransfer> getScheduledTransfers(Long accountId);
}
```

### Interceptors

#### @Audit

Logs method invocations with parameters and results:

```java
@Audit
public void performOperation() {
    // This method call will be logged
}
```

#### @Performance

Tracks method execution time:

```java
@Performance
public void timeCriticalOperation() {
    // Execution time will be logged
}
```

### Timer Services

- **ScheduledFundTransferBean** - Executes scheduled transfers at specified intervals
- **InterestCalculatorBean** - Calculates and applies interest to accounts

---

## 📸 Screenshots

<div align="center">

### Dashboard Overview
![Dashboard](./screenshots/Screenshot-1.png)

### Account Management
![Accounts](./screenshots/Screenshot-2.png)

### Fund Transfer Interface
![Transfer](./screenshots/Screenshot-3.png)

### Transaction History
![History](./screenshots/Screenshot-4.png)

### Scheduled Transfers
![Scheduled](./screenshots/Screenshot-5.png)

### Employee Portal
![Employee](./screenshots/Screenshot-6.png)

### Security & Authentication
![Security](./screenshots/Screenshot-7.png)

### Error Handling
![Error](./screenshots/Screenshot-8.png)

</div>

---

## 🔧 Development

### Building Individual Modules

```bash
# Build core module only
cd core-module
mvn clean install

# Build EJB module
cd ejb-module
mvn clean install

# Build web module
cd web-module
mvn clean install
```

### Running Tests

```bash
# Run all tests
mvn test

# Run tests for specific module
cd core-module
mvn test
```

### IDE Setup

**IntelliJ IDEA:**

1. File → Open → Select project root
2. Maven will automatically import dependencies
3. Configure Payara Server:
   - Settings → Build, Execution, Deployment → Application Servers
   - Add Payara Server installation
4. Run/Debug configurations:
   - Create new "Payara Server" configuration
   - Deploy `bank-app-ear.ear`

---

## 🧪 Testing

### Manual Testing Checklist

- [ ] User registration and login
- [ ] Account creation
- [ ] Fund transfer with OTP verification
- [ ] Scheduled transfer creation and execution
- [ ] Email notification delivery
- [ ] Role-based access control
- [ ] Audit logging functionality
- [ ] Performance monitoring

### Integration Testing

The application is designed for integration testing with:

- Payara Server's embedded container
- JUnit 5 for unit tests
- Arquillian (optional) for integration tests

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit your changes** (`git commit -m 'Add some AmazingFeature'`)
4. **Push to the branch** (`git push origin feature/AmazingFeature`)
5. **Open a Pull Request**

### Code Style

- Follow Java naming conventions
- Use meaningful variable and method names
- Add JavaDoc comments for public methods
- Maintain consistent indentation (4 spaces)

---

## 👨‍💻 Author

**Disura Aberathna**

- GitHub: [@DisuraAberathna](https://github.com/DisuraAberathna)
- Project: [National Bank](https://github.com/DisuraAberathna/national-bank)

---

## 🙏 Acknowledgments

- Jakarta EE Community
- Payara Foundation
- All open-source contributors

---

<div align="center">

### ⭐ Star this repo if you find it helpful!

**Built with ❤️ using Jakarta EE**

</div>
