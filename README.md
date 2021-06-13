# cmake-c-asan-tsan
> A starter C project with Asan & Tsan wired-in

## Build
```sh
mkdir build
cd build
cmake ..
```

## Compile
```sh
cd build
make
```

## Usage
Run the binary compiled with Asan & UBsan
```sh
./main-asan
```

Run the binary compiled with Tsan & UBsan
```sh
./main-tsan
```