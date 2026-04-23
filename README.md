# calc
python base calc


import re


def get_number(prompt: str) -> float:
    while True:
        user_input = input(prompt).strip()
        try:
            return float(user_input)
        except ValueError:
            print("Invalid number. Please try again.")


def calculate(num1: float, num2: float, operator: str) -> float:
    if operator == "+":
        return num1 + num2
    if operator == "-":
        return num1 - num2
    if operator == "*":
        return num1 * num2
    if operator == "/":
        if num2 == 0:
            raise ZeroDivisionError("Cannot divide by zero.")
        return num1 / num2
    raise ValueError("Unsupported operator.")


def parse_expression(expression: str) -> tuple[float, str, float]:
    match = re.fullmatch(r"\s*(-?\d+(?:\.\d+)?)\s*([+\-*/])\s*(-?\d+(?:\.\d+)?)\s*", expression)
    if not match:
        raise ValueError("Invalid expression format.")
    num1, operator, num2 = match.groups()
    return float(num1), operator, float(num2)


def main() -> None:
    print("Simple Python Calculator")
    print("Supported operators: +  -  *  /")
    print("You can enter an expression like anything ")

    first_input = input("Enter expression or first number: ").strip()

    try:
        if re.fullmatch(r"\s*-?\d+(?:\.\d+)?\s*", first_input):
            first_number = float(first_input)
            operator = input("Enter an operator (+, -, *, /): ").strip()
            second_number = get_number("Enter the second number: ")
        else:
            first_number, operator, second_number = parse_expression(first_input)

        result = calculate(first_number, second_number, operator)
        print(f"Result: {result}")
    except (ValueError, ZeroDivisionError) as error:
        print(f"Error: {error}")


if __name__ == "__main__":
    main()
