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
    
    
    
    
    
    
    
    public class Combination
{
    readonly int _count;
    readonly int _numberOfAll;

    readonly int[] _sourceList;
    readonly int[] _emptyIndex;
    int[] _caseIndex;

    int _effectiveCount;

    public Combination(int [] elems)
    {
        _sourceList = elems;
        _count = _sourceList.Length;
        _numberOfAll = (1 << _count);

        _emptyIndex = new int[_count];
        for (int i = 0; i < _count; i ++)
        {
            _emptyIndex[i] = -1;
        }

        _caseIndex = new int[_count];
    }

    public IEnumerable<int []> Successor()
    {
        for (int i = 0; i < _numberOfAll; i ++)
        {
            _effectiveCount = 0;
            Array.Copy(_emptyIndex, _caseIndex, _count);

            for (int c = 0; c < _count; c++)
            {
                int mask = (1 << c); // 이 코드의 간단한 핵심.
                if ((i & mask) == mask)
                {
                    _caseIndex[_effectiveCount] = c;
                    _effectiveCount++;
                }
            }

            yield return _caseIndex;
        }
    }

    public int [] Apply()
    {
        int[] combinations = new int[_effectiveCount];

        for (int i = 0; i < _effectiveCount; i ++)
        {
            combinations[i] = _sourceList[_caseIndex[i]];
        }

        return combinations;
    }
}
