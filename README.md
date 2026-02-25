# Matrix-Reconstruction
Simple code for analyzing and rearranging a matrix

import random

def generate_matrix(rows, cols):
    matrix = []
    for _ in range (rows):
        row = []
        for _ in range(cols):
            row.append(random.randint(1,100))
        matrix.append(row)
    return matrix

def calculate_total_sum(matrix):
    total = 0
    for row in matrix:
        for num in row:
            total += num
    return total

def find_min_max(matrix):
    current_min = matrix[0][0]
    current_max = matrix[0][0]

    for row in matrix:
        for num in row:
            if num < current_min:
                current_min = num
            if num > current_max:
                current_max = num

    return current_min, current_max

def bubble_sort_row(row):
    n = len(row)
    for i in range(n):
        for j in range(0, n - i - 1):
            if row[j] > row[j + 1]:
                row[j], row[j + 1] = row[j + 1], row[j]
    return row

def sort_matrix_rows(matrix):
    for i in range(len(matrix)):
        bubble_sort_row(matrix[i])

def search_value(matrix, target):
    positions = []
    for r_idx, row in enumerate(matrix):
        for c_idx, val in enumerate(row):
            if val == target:
                positions.append((r_idx, c_idx))
                return positions

def main():
    M = 10 
    N = 10 

    print(f"--- 1. Generating {M}x{N} Matrix ---")
    my_grid = generate_matrix(M,N)
    for row in my_grid:
        print(row)


    print ("\n--- 2. Total Sum---")
    total = calculate_total_sum(my_grid)
    print(f"Total Sum: {total}")

    print("\n--- 3. Min and Max ---")
    min_val, max_val = find_min_max(my_grid)
    print(f"Minimum: {min_val}, Maximum: {max_val}")

    print("\n--- 4. Element Search (Before Sort) ---")
    target = min_val
    locs = search_value(my_grid, target)
    print(f"Searching for{target}: found at {locs}")

    print("\n--- 5. Sorting Rows ---")
    sort_matrix_rows(my_grid)
    print("Rows sorted independently:")
    for row in my_grid:
        print(row)

if __name__ == "__main__":
    main()
