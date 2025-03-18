### README for `mailu-collection`

#### Overview
The `mailu-collection` is an Ansible collection designed to manage a Mailu instance via its REST API. It provides roles to configure users, domains, aliases, and alternatives in an idempotent manner. Each role ensures that the specified resources exist, creating them if they do not.

---

### Roles

#### 1. **Domains**
Manages domains in the Mailu instance.

#### 2. **Users**
Manages users (email accounts) in the Mailu instance.

#### 3. **Aliases**
Manages email aliases in the Mailu instance.

#### 4. **Alternatives**
Manages alternative email addresses in the Mailu instance.

---

### Variables

#### Common Variables
These variables are shared across all roles:
- `mailu_api_url`: The base URL of the Mailu API (e.g., `http://mailu.example.com/api`).
- `mailu_api_key`: The API key used for authentication.

#### Role-Specific Variables

##### **Domains**
- `mailu_domains`: A list of domains to manage. Each domain is defined as:
  ```yaml
  mailu_domains:
    - name: "example.com"
    - name: "anotherexample.com"
  ```

##### **Users**
- `mailu_users`: A list of users to manage. Each user is defined as:
  ```yaml
  mailu_users:
    - email: "user1@example.com"
      password: "password1"
      quota: 1000
    - email: "user2@example.com"
      password: "password2"
      quota: 2000
  ```

##### **Aliases**
- `mailu_aliases`: A list of aliases to manage. Each alias is defined as:
  ```yaml
  mailu_aliases:
    - source: "alias1@example.com"
      destination: "user1@example.com"
    - source: "alias2@example.com"
      destination: "user2@example.com"
  ```

##### **Alternatives**
- `mailu_alternatives`: A list of alternative email addresses to manage. Each alternative is defined as:
  ```yaml
  mailu_alternatives:
    - email: "user1@example.com"
      alternatives:
        - "alt1@example.com"
        - "alt2@example.com"
    - email: "user2@example.com"
      alternatives:
        - "alt3@example.com"
  ```

---

### Usage

#### Example Playbook
Below is an example playbook that uses the `mailu-collection` to configure domains and users:

```yaml
- name: Configure Mailu instance
  hosts: localhost
  collections:
    - mailu-collection
  vars:
    mailu_api_url: "http://mailu.example.com/api"
    mailu_api_key: "your_api_key"
    mailu_domains:
      - name: "example.com"
      - name: "anotherexample.com"
    mailu_users:
      - email: "user1@example.com"
        password: "password1"
        quota: 1000
      - email: "user2@example.com"
        password: "password2"
        quota: 2000
  tasks:
    - name: Manage domains
      include_role:
        name: domains

    - name: Manage users
      include_role:
        name: users
```

---

### Installation
1. Clone the collection into your Ansible collections directory:
   ```bash
   ansible-galaxy collection install path/to/mailu-collection
   ```
2. Use the collection in your playbooks by referencing `mailu-collection`.

---

### Notes
- Ensure the Mailu API is accessible and the API key has sufficient permissions.
- The collection is idempotent, meaning it will only make changes if the desired state is not already present.
