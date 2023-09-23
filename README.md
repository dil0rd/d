# d
java калькулятор валют( выполнили студенты УлГУ МОАИС 20/1 Мещанин Дмитрий, Кирилл Беляев, задание java se 2)
import java.util.regex.*;

public class CurrencyCalculator {
    private double dollarToRublesRate;

    public CurrencyCalculator(double dollarToRublesRate) {
        this.dollarToRublesRate = dollarToRublesRate;
    }

    public double toDollars(double rubles) {
        return rubles / dollarToRublesRate;
    }

    public double toRubles(double dollars) {
        return dollars * dollarToRublesRate;
    }

    public double evaluate(String expression) {
        Pattern pattern = Pattern.compile("\\$[0-9]+(\\.[0-9]+)?|\\b[0-9]+(\\.[0-9]+)?р\\b");
        Matcher matcher = pattern.matcher(expression);

        while (matcher.find()) {
            String match = matcher.group();

            if (match.contains("$")) {
                double dollars = Double.parseDouble(match.substring(1));
                expression = expression.replace(match, String.valueOf(dollars));
            } else {
                double rubles = Double.parseDouble(match.substring(0, match.length() - 1));
                expression = expression.replace(match, String.valueOf(toDollars(rubles)));
            }
        }

        return evaluateExpression(expression);
    }

    private double evaluateExpression(String expression) {
        return new java.util.Scanner(expression).useDelimiter("\\s+").nextDouble();
    }

    public static void main(String[] args) {
        double dollarToRublesRate = 60.0; // Установите курс доллара к рублю здесь

        CurrencyCalculator calculator = new CurrencyCalculator(dollarToRublesRate);

        String input = "toDollars(737р + toRubles($85.4))";
        double result = calculator.evaluate(input);

        System.out.println(result + "р");
    }
}
