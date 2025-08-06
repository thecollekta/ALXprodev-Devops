# Pokémon API Automation

A set of shell scripts to automate:

1. Fetching Pokémon data from PokeAPI (`apiAutomation-0x00`)
2. Extracting key details from the response (`data_extraction_automation-0x01`)
3. Batch processing with retry logic (`batchProcessing-0x02`)
4. Generating summary reports (`summaryData-0x03`)
5. Parallel data fetching (`batchProcessing-0x04`)

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
   - Handles unit conversions (decimeters to meters, hectograms to kg)

3. `batchProcessing-0x02`:
   - Fetches data for multiple Pokémon in sequence
   - Implements retry logic (3 attempts per Pokémon)
   - Creates a `pokemon_data` directory for output
   - Includes rate limiting (1s between requests)
   - Provides detailed error messages and logging

4. `summaryData-0x03`:
   - Processes all JSON files in `pokemon_data`
   - Generates a CSV report with metrics
   - Calculates average height and weight
   - Handles missing files gracefully
   - Properly formats numeric output

5. `batchProcessing-0x04`:
   - Downloads Pokémon data in parallel
   - Configurable concurrency level (default: 3)
   - Progress tracking and status updates
   - Error handling and validation
   - Summary of download results

---

## Prerequisites/Requirements

- Bash shell
- `curl` for HTTP requests
- `jq` for JSON processing
- `awk` for text processing
- `sed` for text transformations
- Internet connection

---

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/ALXprodev-Devops.git
cd ALXprodev-Devops/Advanced_shell

# Make scripts executable
chmod +x apiAutomation-0x00 data_extraction_automation-0x01 \
     batchProcessing-0x02 summaryData-0x03 batchProcessing-0x04
```

---

## Usage

### 1. Fetch Single Pokémon Data

```bash
./apiAutomation-0x00
```

### 2. Extract Pokémon Details

```bash
./data_extraction_automation-0x01
```

### 3. Batch Process Multiple Pokémon

```bash
# Default behavior (with retries)
./batchProcessing-0x02
```

### 4. Generate Summary Report

```bash
./summaryData-0x03
```

### 5. Parallel Processing

```bash
# Default (3 concurrent downloads)
./batchProcessing-0x04

# Custom concurrency (e.g., 5)
MAX_CONCURRENT=5 ./batchProcessing-0x04
```

---

## Output Files

- `data.json`: Raw API response for single Pokémon
- `errors.txt`: Error logs (if any)
- `pokemon_data/`: Directory containing individual Pokémon JSON files
- `pokemon_report.csv`: Summary report with metrics

---

## Error Handling

All scripts include comprehensive error handling:

- Network timeouts
- Invalid responses
- File system operations
- API rate limiting
- JSON parsing errors

---

## Best Practices

1. **Error Logging**: All errors are logged with timestamps
2. **Idempotency**: Scripts can be safely re-run
3. **Resource Management**: Proper cleanup of temporary files
4. **Input Validation**: All inputs are validated
5. **Documentation**: Clear usage instructions and examples

---

## Troubleshooting

1. **Permission Denied**

   ```bash
   chmod +x script_name
   ```

2. **Command Not Found**
   Ensure required tools are installed:

   ```bash
   # On Ubuntu/Debian
   sudo apt-get install curl jq
   
   # On macOS
   brew install curl jq
   ```

3. **API Rate Limiting**
   - The scripts include built-in rate limiting
   - For parallel processing, adjust `MAX_CONCURRENT` if needed

---

## License

This project is for educational purposes under the ALX ProDEV BE Curriculum Program.

---

## Sample Outputs

### Data Extraction

```bash
Pikachu is of type Electric, weighs 6kg, and is 0.4m tall.
```

### Batch Processing

```bash
Fetching data for bulbasaur...
Saved data to pokemon_data/bulbasaur.json
Fetching data for ivysaur...
Attempt 1 failed for ivysaur
Retrying in 1 second...
Saved data to pokemon_data/ivysaur.json
```

### Summary Report

```bash
CSV Report generated at: pokemon_report.csv

Name,Height (m),Weight (kg)
Bulbasaur,0.7,6.9
Charmander,0.6,8.5
Ivysaur,1.0,13.0
Venusaur,2.0,100.0

Average Height: 1.08 m
Average Weight: 29.48 kg
```

### Parallel Processing

```bash
Processing bulbasaur 
Starting download for bulbasaur...
Successfully downloaded bulbasaur

Processing ivysaur 
Starting download for ivysaur...
Successfully downloaded ivysaur

Processing venusaur 
Starting download for venusaur...
Successfully downloaded venusaur

Processing charmander 
Starting download for charmander...
Successfully downloaded charmander

Processing charmeleon 
Starting download for charmeleon...
Successfully downloaded charmeleon

Download Summary:
Total Pokémon: 5
Successfully downloaded: 5
Failed downloads: 0
All downloads completed successfully!
```
