# Tab, Tab, Attack

- **Event:** picoCTF 2021
- **Author:** syreal
- **Category:** General Skills
- **Difficulty:** Easy
- **Challenge:** Use tab completion in the Terminal to navigate long directory structures and filenames.
- **Archive:** [Addadshashanammu.zip](https://challenge-files.picoctf.net/c_wily_courier/c090282eec93405912f926586287741dd5b9bd24cbdf8f3555c53902d556e508/Addadshashanammu.zip)

## Problem Statement

The challenge provides a ZIP archive containing a deeply nested directory structure. The goal is to find the relevant file and inspect it for the flag.

## Finding the File

I used `find` to search the extracted directories for the file named `fang-of-haynekhtnamet.c`:

```bash
find -name "fang-of-haynekhtnamet.c"
```

The command returned this path:

```text
./Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/fang-of-haynekhtnamet.c
```

## Solution

I changed into the directory containing the source file:

```bash
cd Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku/
```

The directory contained both the source file and a compiled binary:

```bash
ls
```

```text
fang-of-haynekhtnamet  fang-of-haynekhtnamet.c
```

I read the C source with `cat`:

```bash
cat fang-of-haynekhtnamet.c
```

The source printed the flag with `printf`:

```c
printf("*ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_fc588427}\n");
```

## Flag

```text
picoCTF{l3v3l_up!_t4k3_4_r35t!_fc588427}
```

## Takeaways

- `find` can locate a file without manually traversing every directory.
- Tab completion helps navigate long paths and filenames efficiently.
- Source files can reveal program output directly, especially when the flag is passed to `printf`.