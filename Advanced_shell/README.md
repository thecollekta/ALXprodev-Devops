# Pokémon API Request Automation

A shell script to automate fetching Pokémon data from the PokeAPI and handling the response.

---

## Features/Description

This project contains a Bash script that:

- Makes an API request to fetch Pikachu's data from the Pokémon API
- Saves successful responses to `data.json`
- Logs errors to `errors.txt` if the request fails
- Includes proper cleanup of stale files

---

## Prerequisites/Requirements

- Bash shell
- `curl` command-line tool
- Internet connection

---

## Installation

No installation required. Just download the script:

```bash
wget https://raw.githubusercontent.com/yourusername/ALXprodev-Devops/main/Advanced_shell/apiAutomation-0x00
```

---

## Usage

1. Make the script executable:

    ```bash
    chmod +x apiAutomation-0x00
    ```

2. Run the script:

    ```bash
    ./apiAutomation-0x00
    ```

3. Check the output:
    - Successful responses are saved to `data.json` with Pikachu's data and removes any
    existing `errors.txt`
    - Failure creates or updates `errors.txt` with details and removes any existing `data.json`

---

## Sample Output

- `data.json`: Contains the complete Pokémon data in JSON format
- `errors.txt`: Logs any errors that occur during execution

### Example

```bash
./apiAutomation-0x00
```

```json
Successfully retrieved Pikachu data
Data saved to data.json
{
  "abilities": [
    {
      "ability": {
        "name": "static",
        "url": "https://pokeapi.co/api/v2/ability/9/"
      },
      "is_hidden": false,
      "slot": 1
    },
```

---

## Error Handling

If the API request fails, check errors.txt for details:

```bash
cat errors.txt
```

---

## License

This project is for educational purposes under the ALX ProDEV BE Curriculum Program.
