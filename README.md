task2
class Solution {
    public int sumOfTheDigitsOfHarshadNumber(int x) {
        int sum = 0;
        int temp = x;
        while (temp > 0) {
            sum += temp % 10;
            temp /= 10;
        }

        if (x % sum == 0) {
            return sum;
        } else {
            return -1;
        }
    }
}


task 3
import java.io.*;
import java.util.*;

public class Main {

    static final int MAX = 1000000;

    public static void main(String[] args) throws Exception {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringBuilder output = new StringBuilder();

        // Step 1: Mark generated numbers
        boolean[] generated = new boolean[MAX + 1];

        for (int i = 1; i <= MAX; i++) {
            int sum = i;
            int temp = i;

            while (temp > 0) {
                sum += temp % 10;
                temp /= 10;
            }

            if (sum <= MAX) {
                generated[sum] = true;
            }
        }

        // Step 2: Sieve of primes
        boolean[] isPrime = new boolean[MAX + 1];
        Arrays.fill(isPrime, true);

        isPrime[0] = isPrime[1] = false;

        for (int i = 2; i * i <= MAX; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j <= MAX; j += i) {
                    isPrime[j] = false;
                }
            }
        }

        // Step 3: Prefix array for Devlali primes
        int[] prefix = new int[MAX + 1];

        for (int i = 1; i <= MAX; i++) {
            prefix[i] = prefix[i - 1];

            if (!generated[i] && isPrime[i]) {
                prefix[i]++;
            }
        }

        // Step 4: Answer queries
        int Q = Integer.parseInt(br.readLine());

        while (Q-- > 0) {
            String[] parts = br.readLine().split(" ");
            int A = Integer.parseInt(parts[0]);
            int B = Integer.parseInt(parts[1]);

            int result = prefix[B] - (A > 0 ? prefix[A - 1] : 0);
            output.append(result).append("\n");
        }

        System.out.print(output);
    }
}
