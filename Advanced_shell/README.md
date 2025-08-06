# Pokémon API Request Automation

A set of shell scripts to automate:

1. Fetching Pokémon data from PokeAPI (`apiAutomation-0x00`)
2. Extracting key details from the response (`data_extraction_automation-0x01`)
3. Batch processing script fetches data for multiple Pokémon and saves each to a separate JSON file (`batchProcessing-0x02`)

---

## Features/Description

### Scripts

1. `apiAutomation-0x00`:
    - Fetches Pikachu data from Pokémon API
    - Saves response to `data.json` on success
    - Logs errors to `errors.txt` on failure
    - Cleans up stale files automatically

2. `data_extraction_automation-0x01`:
    - Parses `data.json` using `jq`
    - Extracts name, height, weight, and primary type
    - Formats output:  
    `Pikachu is of type Electric, weighs 6kg, and is 0.4m tall.`
    - Enhanced Error Handling:
      - Implements 3 retry attempts for failed API requests
      - 1-second delay between retries
      - Detailed error diagnostics stored in `errors.txt`
      - Clear status messages for each retry attempt
      - Final failure message after 3 unsuccessful attempts

3. `batchProcessing-0x02`:
    - Fetches data for multiple Pokémon in sequence
    - Creates a `pokemon_data` directory for output
    - Includes rate limiting to prevent API abuse
    - Provides clear status messages
    - Handles errors gracefully

4. `summaryData-0x03`:
    - Reads all JSON files from the `pokemon_data` directory
    - Extracts name, height, and weight for each Pokémon
    - Generates a CSV file with the collected data
    - Calculates and displays average height and weight
    - Handles missing or empty directories gracefully

---

## Prerequisites/Requirements

- Bash shell
- `curl` command-line tool
- `jq` (for JSON parsing)
- Internet connection

---

## Installation

No installation required. Just download the script:

```bash
# Download scripts
wget https://github.com/yourusername/ALXprodev-Devops/main/Advanced_shell/apiAutomation-0x00
wget https://github.com/yourusername/ALXprodev-Devops/main/Advanced_shell/data_extraction_automation-0x01
```

---

## Usage

1. Make the script executable:

    ```bash
    # Make executable
    chmod +x apiAutomation-0x00 data_extraction_automation-0x01 batchProcessing-0x02 summaryData-0x03
    ```

2. Run the script:

    ```bash
    # Fetch Data
    ./apiAutomation-0x00

    # Extract Pokémon Data
    ./data_extraction_automation-0x01

    # Batch Processing
    ./batchProcessing-0x02

    # Summary Data
    ./summaryData-0x03

    # Error Handling
    ./batchProcessing-0x02
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
// Successfully retrieved Pikachu data
// Data saved to data.json
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

```bash
$ ./data_extraction_automation-0x01
Pikachu is of type , weighs 0kg, and is 0.0m tall.
0.4 is of type , weighs 0kg, and is 0.0m tall.
6 is of type , weighs 0kg, and is 0.0m tall.
Electric is of type , weighs 0kg, and is 0.0m tall.
```

```bash
$ ./batchProcessing-0x02
Fetching data for bulbasaur...
Saved data to pokemon_data/bulbasaur.json
Fetching data for ivysaur...
Saved data to pokemon_data/ivysaur.json
Saved data to pokemon_data/venusaur.json
Fetching data for charmander...
Saved data to pokemon_data/charmander.json
Fetching data for charmeleon...
Saved data to pokemon_data/charmeleon.json
```

```bash
./summaryData-0x03
CSV Report generated at: pokemon_report.csv

Name,Height (m),Weight (kg)
Bulbasaur,0.7,6.9
Charmander,0.6,8.5
Ivysaur,1.0,13.0
Venusaur,2.0,100.0

Average Height: 1.08 m
Average Weight: 29.48 kg
```

```bash
./batchProcessing-0x02
Fetching data for bulbasaur...
Saved data to pokemon_data/bulbasaur.json
Fetching data for ivysaur...
Saved data to pokemon_data/ivysaur.json
Fetching data for venusaur...
Saved data to pokemon_data/venusaur.json
Fetching data for charmander...
Saved data to pokemon_data/charmander.json
Fetching data for charmeleon...
Saved data to pokemon_data/charmeleon.json
```

---

## Error Handling

If the API request fails, check `errors.txt` for details:

```bash
cat errors.txt
```

- `apiAutomation-0x00`: Errors saved to errors.txt
- `data_extraction_automation-0x01`:
  - Fails silently if data.json missing
  - Outputs nothing if required fields absent
- `batchProcessing-0x02`:
  - Failed requests logged to stderr
  - Script continues processing next Pokémon after failures

---

## License

This project is for educational purposes under the ALX ProDEV BE Curriculum Program.
