# combination
조합(순서 보장) / 소수 체크 함수 예제 , 조합(모든 경우)












    public class Solution123
    {
        static string[] combination(string s)
        {
            char[] orderedArray = s.ToCharArray().Distinct().OrderBy(o => o).ToArray();
            List<string> result = new List<string>();
            for (int k = 0; k < orderedArray.Length; ++k)
            {
                string prefix = "";
                for (int i = k; i < orderedArray.Length; ++i)
                {
                    prefix = k == i ? orderedArray[i].ToString() : prefix + orderedArray[i].ToString();
                    result.Add(prefix);
                    for (int j = i + 1; j < orderedArray.Length; ++j)
                    {
                        result.Add(prefix + orderedArray[j].ToString());
                    }
                }
            }
             result = result.Distinct().ToList();
             
            return result.ToArray();

        }

        public static int solution(int[] nums)
        {
            int answer = 0;

            List<int> checkList = new List<int>();
            string s = "";
            for (int i = 0; i < nums.Length; ++i)
            {
                s += nums[i].ToString();
            }
            Console.WriteLine(s);
            Array.ForEach(combination(s), delegate (string p)
            {
                Console.WriteLine(p);
                if (p.Length == 3)
                {
                    checkList.Add(int.Parse(p));
                }
            });
            foreach (int i in checkList)
            {
                if (isPrime(i) == 1)
                    answer++;
            }
            return answer;
        }

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
