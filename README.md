import csv
import statistics

def load_csv(file_path):
    try:
        with open(file_path, newline='') as csvfile:
            reader = csv.DictReader(csvfile)
            data = [row for row in reader]
            return data
    except FileNotFoundError:
        print("File not found.")
        return []

def get_column_numbers(data, column):
    try:
        return [float(row[column]) for row in data if row[column]]
    except KeyError:
        print(f"Column '{column}' not found.")
        return []

def print_stats(numbers):
    if not numbers:
        print("No data to analyze.")
        return
    print(f"Count: {len(numbers)}")
    print(f"Mean: {statistics.mean(numbers):.2f}")
    print(f"Median: {statistics.median(numbers):.2f}")
    print(f"Standard Deviation: {statistics.stdev(numbers):.2f}")

def main():
    print("Welcome to CSV Analyzer!")
    file_path = input("Enter CSV file path: ")
    column = input("Enter column name to analyze: ")

    data = load_csv(file_path)
    numbers = get_column_numbers(data, column)
    print_stats(numbers)

if __name__ == "__main__":
    main()

