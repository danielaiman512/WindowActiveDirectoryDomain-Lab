# Validation and Testing

## 1. Purpose

This document records the validation performed after building the Windows Server 2025 Active Directory environment.

The objective is to verify that:

- DC01 is configured correctly.
- Active Directory is functioning.
- DNS is resolving domain names.
- CLIENT01 can communicate with DC01.
- CLIENT01 is joined to company.com.
- The helpdesk1 account can authenticate.

## 2. Test Environment

| Component | Value |
|---|---|
| Domain Controller | DC01 |
| Domain | company.com |
| DC01 IPv4 | 10.0.0.1 |
| Client | CLIENT01 |
| Client IPv4 | 10.0.0.2 |
| Domain User | helpdesk1 |

## 3. Network Configuration Test

### Test 1 — Verify DC01 IPv4 Configuration

**Procedure**

On DC01, open Command Prompt and run:

```cmd
ipconfig /all
```

**Expected Result**

DC01 should display:

- IPv4 address: 10.0.0.1
- Subnet mask: 255.255.255.0
- DNS server: 127.0.0.1

**Purpose**

This confirms that the Domain Controller has the expected static network configuration.

**Evidence**

`docs/evidence/02-dc01-static-ip.png`

### Test 2 — Verify CLIENT01 IPv4 Configuration

**Procedure**

On CLIENT01, run:

```cmd
ipconfig /all
```

**Expected Result**

CLIENT01 should display:

- IPv4 address: 10.0.0.2
- Subnet mask: 255.255.255.0
- DNS server: 10.0.0.1

**Purpose**

This confirms that the client uses DC01 as its DNS server.

**Evidence**

`docs/evidence/07-client01-ip.png`

## 4. DNS Validation

### Test 3 — Resolve DC01 by Fully Qualified Domain Name

**Procedure**

On CLIENT01, run:

```cmd
nslookup dc01.company.com
```

**Expected Result**

The DNS response should resolve DC01 to:

`10.0.0.1`

**Purpose**

This confirms that the client can resolve the Domain Controller through DNS.

### Test 4 — Verify the Domain DNS Zone

**Procedure**

On DC01:

1. Open DNS Manager.
2. Expand Forward Lookup Zones.
3. Select company.com.
4. Verify that DC01 has a valid host record.

**Expected Result**

The company.com zone exists and contains the required DNS records.

**Purpose**

This confirms that the DNS zone was created during Domain Controller promotion.

**Evidence**

`docs/evidence/05-dns-zone.png`

## 5. Active Directory Validation

### Test 5 — Verify the Domain User

**Procedure**

On DC01:

1. Open Active Directory Users and Computers.
2. Select the Users container.
3. Locate helpdesk1.
4. Open the account properties.

**Expected Result**

The helpdesk1 account exists and is enabled.

**Purpose**

This confirms that the user account was successfully created in Active Directory.

**Evidence**

`docs/evidence/06-helpdesk1-account.png`

### Test 6 — Verify the Client Computer Account

**Procedure**

On DC01:

1. Open Active Directory Users and Computers.
2. Select the Computers container.
3. Locate CLIENT01.

**Expected Result**

CLIENT01 appears as a computer object in the domain.

**Purpose**

This confirms that the client was registered in Active Directory during the domain join process.

## 6. Domain Membership Validation

### Test 7 — Confirm CLIENT01 Domain Membership

**Procedure**

On CLIENT01:

1. Open Settings.
2. Select System.
3. Select About.
4. Verify the domain membership.

**Expected Result**

CLIENT01 is joined to:

`company.com`

**Evidence**

`docs/evidence/09-client01-domain-membership.png`

## 7. Domain Authentication Validation

### Test 8 — Sign In Using helpdesk1

**Procedure**

On CLIENT01:

1. Sign out.
2. Select Other user.
3. Enter COMPANY\helpdesk1.
4. Enter the account password.
5. Sign in.

**Expected Result**

The user successfully logs in and Windows creates the user's profile.

**Purpose**

This confirms that the domain user can authenticate against Active Directory.

**Evidence**

`docs/evidence/10-helpdesk1-domain-login.png`

## 8. Final Validation Summary

Complete this table after performing the tests.

| Test | Result |
|---|---|
| DC01 static IP configuration | Passed |
| CLIENT01 static IP configuration | Passed |
| DNS resolution of DC01 | Passed |
| Active Directory domain creation | Passed |
| helpdesk1 account creation | Passed |
| CLIENT01 domain membership | Passed |
| helpdesk1 domain authentication | Passed |

The test results above represent the expected successful outcome. I record the actual results after performing each test.

## 9. Final Result

The environment is considered successfully configured when CLIENT01 can resolve DC01 through DNS, is joined to company.com, and allows helpdesk1 to sign in using domain credentials.

This demonstrates the basic operation of a Windows Active Directory domain environment.
