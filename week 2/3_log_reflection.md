AI OUTPUT + KEEP/MODIFY/REJECT

Here is a complete, copy-pasteable Python script using the pandas library. It loads your file and runs all four checks (duplicates, missing values, data types, and value counts of 24).
python
import pandas as pd

# 1. Load your file
# Replace 'your_file.csv' with your actual file name.
# If it is an Excel file, use: df = pd.read_excel('your_file.xlsx')
df = pd.read_csv('your_file.csv')

print("--- 1. DUPLICATE CHECK ---")
exact_dupes = df.duplicated().sum()
print(f"Exact duplicate rows found: {exact_dupes}")
** KEEP **

# Optional: Check duplicates based on specific columns (e.g., same date, item, and city)
subset_dupes = df.duplicated(subset=['date', 'item', 'city']).sum()
print(f"Duplicate entries for same date/item/city: {subset_dupes}")
** MODIFY **

# Remove exact duplicates (uncomment the line below if you want to drop them)
# df = df.drop_duplicates()


print("\n--- 2. UNAVAILABLE / MISSING ENTRIES ---")
# Count standard blank cells (NaN/None)
missing_counts = df.isnull().sum()
print("Standard missing values per column:")
print(missing_counts)
** KEEP **

# Check for text placeholders like 'N/A', 'NA', 'null', '-', or 'unavailable'
placeholders = ['n/a', 'na', 'null', 'none', '-', 'unavailable', '']
for col in df.columns:
    # Convert to string, lowercase, and strip spaces to catch hidden text placeholders
    bad_entries = df[col].astype(str).str.strip().str.lower().isin(placeholders).sum()
    if bad_entries > 0:
        print(f"Column '{col}' has {bad_entries} text-based unavailable entries.")
** REJECT ** -- Couldnt explain or understand


print("\n--- 3. DATA TYPE CHECK & FIX ---")
print("Current data types:")
print(df.dtypes)
** MODIFY **

# Check if 'date' converts cleanly to datetime
parsed_dates = pd.to_datetime(df['date'], errors='coerce')
invalid_dates = parsed_dates.isnull().sum() - df['date'].isnull().sum()
print(f"\nInvalid date formats found: {invalid_dates}")
** KEEP ** 
# Check if 'price' converts cleanly to numbers (float)
# Strip currency symbols or commas just in case before checking
clean_price = df['price'].astype(str).str.replace(r'[$,]', '', regex=True)
parsed_prices = pd.to_numeric(clean_price, errors='coerce')
invalid_prices = parsed_prices.isnull().sum() - df['price'].isnull().sum()
print(f"Invalid price formats found: {invalid_prices}")
** MODIFY also kinda reject **

print("\n--- 4. VALUE COUNT CHECK (TARGET = 24) ---")
# Check if each unique item, city, or date appears exactly 24 times
columns_to_check = ['item', 'city', 'date', 'data_label']

for col in columns_to_check:
    counts = df[col].value_counts()
    not_24 = counts[counts != 24]
    
    if not_24.empty:
        print(f"SUCCESS: All unique values in '{col}' have a count of 24.")
    else:
        print(f"WARNING: The following values in '{col}' do NOT have a count of 24:")
        print(not_24)
        print("-" * 30)

** REJECT ** -- Couldnt understand or explain 

No valid observation was removed 

comparisions is 2_work.ipynb 

*****************************************************
REFLECCTION 
I wouldve missed that every item should appear 24 times, though i couldnt understand the code and decided not to use it 