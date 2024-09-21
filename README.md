public class NumberToWords {

    private static final String[] to_19 = {"", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten", 
        "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen"};
    
    private static final String[] tens = {"", "", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", "eighty", "ninety"};
    
    private static final String[] scales = {"", "thousand", "million"};
    
    public static String convertHundred(int n) {
        if (n < 20) {
            return to_19[n];
        } else if (n < 100) {
            return tens[n / 10] + (n % 10 != 0 ? " " + to_19[n % 10] : "");
        } else {
            return to_19[n / 100] + " hundred" + (n % 100 != 0 ? " " + convertHundred(n % 100) : "");
        }
    }
    
    public static String numberToWords(int num) {
        if (num == 0) {
            return "zero";
        }
        
        StringBuilder words = new StringBuilder();
        int chunkCounter = 0;
        
        while (num > 0) {
            int chunk = num % 1000;
            num /= 1000;
            if (chunk > 0) {
                if (words.length() > 0) {
                    words.insert(0, " ");
                }
                words.insert(0, convertHundred(chunk) + (scales[chunkCounter].isEmpty() ? "" : " " + scales[chunkCounter]));
            }
            chunkCounter++;
        }
        
        return words.toString().trim();
    }

    public static void main(String[] args) {
        System.out.println(numberToWords(1000));         // Output: "one thousand"
        System.out.println(numberToWords(4003));         // Output: "four thousand three"
        System.out.println(numberToWords(999999999));    // Output: "nine hundred ninety-nine million nine hundred ninety-nine thousand nine hundred ninety-nine"
    }
