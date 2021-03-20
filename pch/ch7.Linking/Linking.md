footer: Copyright © 2021 by HungryDev, All rights reserved
slidenumbers: true
autoscale: true
slide-transition: true
build-lists: true

# Linking

---

## Intro

- 링킹은 여러 코드와 데이터를 메모리에 로드되고 실행될 수 있는 하나의 파일로 만드는 과정
- 총 3가지 경우
	- 컴파일 타임(소스 코드가 머신코드로 바뀔 때)
	- 로드 타임(프로그램이 메모리에 올라가고 로더에 의해 실행될때)
	- 런타임(프로그램 동작)

---

## Intro

- 예전에는 링킹을 직접 했다. (Manually)
- 현대 시스템은 링커라는 프로그램이 자동적으로 수행해줌

---

## 7.1 Compiler Drivers

- 대부분 시스템들은 컴파일러 드라이버를 제공합니다.
- 컴파일러 드라이버는 크게 4가지로 구성.
	- Preprocessor(전처리기)
	- Compiler
	- Assembler
	- Linker

---

## 7.1 Compiler Drivers

- GNU 컴파일러 시스템을 활용해 프로그램을 빌드하는 예시

```sh
linux> gcc -Og -o prog main.c sum.c
```

---

## 7.1 Compiler Drivers

### C preprocessor(cpp)

- `main.c`를 `main.i`로 변경

```sh
cpp [other arguments main.c /tmp/main.i]
```

---

## 7.1 Compiler Drivers

### C Compiler(cc1)

- `main.i`를 `main.s`로 변경
- `main.s`는 ASCII assembly 파일

```sh
cc1 /tmp/main.i -Og [other arguments] -o /tmp/main.s
```

---

## 7.1 Compiler Drivers

### Assembler(as)

- `main.s`를 `main.o`로 변경
- `main.o`는 relocatable binary 파일

```sh
as [other arguments] -o /tmp/main.o /tmp/main.s
```

---

## 7.1 Compiler Drivers

### Linker

- `main.o`와 `sum.o`를 결합
- `prog`라는 실행가능한 오브젝트파일 생성

```sh
ld -o prog [system object files and args] /tmp/main.o /tmp/sum.o
```

---

## 7.1 Compiler Drivers

- `prog`를 돌리기위해 리눅스 쉘에서는 해당 파일의 이름을 입력

```sh
./prog
```

---

## 7.1 Compiler Drivers

- 쉘은 loader라 불리는 운영체제상 함수를 통해 프로그램의 시작에 제어권을 넘김
- 로더는 `prog` 파일의 코드와 데이터를 메모리에 복사하는 역할
- 시스템 콜 `execve`

---

## 7.2 Static Linking

- Symbol Re

