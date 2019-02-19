# Branches
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.regex.*;

public class Solution {

    // Complete the superDigit function below.
    static int superDigit(String n, int k) {
        StringBuilder strBuf = new StringBuilder(n);
        return sumarDigitos(strBuf, k);
    }

    static int sumarDigitos(StringBuilder n, int k) 
    {          
        if (n.length() > 999) {
            StringBuilder strBuilder1 = new StringBuilder(n.substring(0, 999));
            StringBuilder strBuilder2 = new StringBuilder(n.substring(999, n.length()));
            int a = sumarDigitos(strBuilder1, k);
            int b = sumarDigitos(strBuilder2, k);
            return sumarDigitos(new StringBuilder(Integer.toString(a + b)), k);
        } else {
            if (n.length() == 1) {
                return Integer.parseInt(n.toString()) * k;
            } 
            
            StringBuilder a = new StringBuilder(n.substring( n.length() - 1, n.length()));
            int i = sumarDigitos(new StringBuilder(n.substring(0, n.length() - 1)), k) ;
            if (n.length() <= 999) {
                return sumarDigitos(new StringBuilder(Integer.toString((Integer.parseInt(a.toString()) * k) + i)), 1);
            } else {
                return (Integer.parseInt(a.toString()) * k) + i;
            }
        }
    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] nk = scanner.nextLine().split(" ");

        String n = nk[0];

        int k = Integer.parseInt(nk[1]);

        int result = superDigit(n, k);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}
