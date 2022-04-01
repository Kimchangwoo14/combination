# combination 소수 체크 함수 예제 , 조합(모든 경우)









 static int isPrime(int n)
        {
            if (n <= 1)
                return 0;

            if (n % 2 == 0)
                return n == 2 ? 1 : 0;

            for (int i = 3; i <= Math.Sqrt(n); i += 2)
            {
                if (n % i == 0)
                    return 0;
            }
            return 1;
        }
    
    
    
    
    ---------------------------------------------------------------------------------------------------------------------------------------------





public static void RunTest()
        {
            StringBuilder sb = new StringBuilder();
            StringCombination("ABC", sb, 0);
        }

        static void StringCombination(string s, StringBuilder sb, int index)
        {
            for (int i = index; i < s.Length; i++)
            {
                // 1) 한 문자 추가
                sb.Append(s[i]);

                // 2) 구한 문자조합 출력
                Console.WriteLine(sb.ToString());

                // 3) 나머지 문자들에 대한 조합 구하기
                StringCombination(s, sb, i + 1);

                // 위의 1에서 추가한 문자 삭제 
                sb.Remove(sb.Length - 1, 1);
            }
        }
