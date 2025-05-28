# Difference between CUBC (Common Use Base Cosmolang) and Cosmolang Core

```js
public class void static memory load "interup" MAIN(::main/mem::64FAT? => {
  public void static _main::Main(iostd::String.for(args[*]Print)) => ({
    public void stability memory SET CLI::console.Print({} => [for i in range(of PRINT in args[*][0]+)o... (=!== 0::10::stmt) in i EOR in t == THEN to ACTION]{
      CodSin: {
        Ints := i + MEM args[]::main = 0 run Print(i.mem.load());
      };
    });
  });
});
/**
 * "interup" MAIN(::main/mem::64FAT ? =>) is for loading something from the disk - ? abb. from if this.
 * i.mem.load() -> read and print.
 * and the rest should be clear
*/
```

Prototypes
```js
public class void static main {
    public static _main Main(String[] args) {
        if (MEMORY.has64FAT()) {
            for (int index = 0; index < MEM.length && index < args.length;) {
                String arg = args[index];
                if (isPrintFormat(arg)) {
                    // Check flag condition
                    int flag = checkFlagCondition();
                    if (flag) {
                        printNumber(args[index].mem.load());
                    }
                } else if (arg.equals("0")) {
                    break;
                }
            }
        }
    }

    private static void printNumber(int value) {
        Ints = 0; // Assuming this initializes some array
        Print(value);
    }

    private static boolean isPrintFormat(String arg) {
        // Implement the PRINT format check here (regex or specific criteria)
        return arg.matches("\\d+"); // Example: checks for digits only
    }
    
    private static int checkFlagCondition() {
        // Replace with actual condition logic, e.g., bitwise operations on a flag variable
        volatile boolean someFlag = false; // Placeholder
        someFlag ^= 1; // Toggle the flag each time
        return someFlag;
    }
}

```

```js
/**
 * "interup" MAIN(::main/mem::64FAT? =>) is for loading something from the disk - ? abbreviation: if this memory type.
 * Processes command-line arguments in PRINT format up to MEM limit (10).
 * For each valid argument, loads and prints an integer from memory via i.mem.load().
 */

// Check if 64FAT memory is available; if so, run main function
::main/mem/64FAT? => {
    public void static _main/Main(String[] parsedArgs) => ({
        // Print initial data using CodSin block equivalent to initializing and printing zero from memory.
        public void stability/CodSin({
            Ints := 0;
            printZero(); // Assume this is a function call
        });

        // Process each argument in PRINT format up to MEM limit (10)
        [for index in 0..MEM-1] {
            if args[index] matches "PRINT" format and flagCondition() then {
                loadAndPrint(index);
            } else if args[index].equals("0") { break; }
        });
    });
};

public void static printZero() => ({
    Ints := 0;
    Print(i.mem.load());
});

// Function to check some condition (originally using EOR and THEN)
public boolean flagCondition() => ({ volatile boolean testFlag = false; testFlag ^= 1; return testFlag; });

// Function to load and print the integer from memory for a given index
public void static loadAndPrint(int idx) => ({
    String valueString = args[idx].mem.load();
    int value = Integer.parseInt(valueString);
    Print(value);
});

```

New
```js
// Check if 64FAT memory exists; if so, run this main function
::main/mem/64FAT? => {
    public void static _main/Main(String[] parsedArgs) => ({
        // Initialize variables in CodSin block equivalent to the original setup
        public void stability/CodSin({
            Ints := 0;
            printZero(); // Print initial memory value (assumed to be zero)
        });

        // Process each argument up to MEM limit (10), checking for valid PRINT format and a flag condition
        [for index in 0..MEM-1] {
            if args[index].matchesPrint() && checkFlagCondition() then {
                loadAndPrintFromIndex(index);
            } else if args[index].equals("0") { break; }
        });
    });
});

// Function to print the initial zero value from memory
public void static printZero() => ({
    Ints := 0;
    int value = i.mem.load();
    Print(value);
});

// Checks for valid PRINT format (e.g., numeric strings)
public boolean matchesPrint(String arg) => ({ 
    return Integer.parseInt(arg.trim()) != null; // Parses to check if non-zero and numeric
});

// Toggles a flag using bitwise XOR operation as in original EOR logic
public boolean checkFlagCondition() => ({
    volatile boolean testFlag = false;
    testFlag ^= 1;
    return testFlag;
});

// Loads value from memory for given index and prints it
public void static loadAndPrintFromIndex(int idx) => ({
    String valueString = args[idx].mem.load();
    int value = Integer.parseInt(valueString);
    Print(value);
});

```
