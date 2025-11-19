using System.Diagnostics;
class Program
{
    static int check1()
    {
        int q;
        while (!int.TryParse(Console.ReadLine(), out q) || q > 4 || q < 1)
        {
            Console.WriteLine("!!!Введите целое число от 1 до 4!!!");
        }
        return q;
    }
    static int InputMassive()
    {
        Console.Write("Введите количество элементов в массиве:");
        int el;
        while (!int.TryParse(Console.ReadLine(), out el) || (el <= 0))
        {
            Console.WriteLine("Ошибка, введите целое положительное число!");
        }
        return el;
    }
    static double check()
    {
        double numb;
        while (!double.TryParse(Console.ReadLine(), out numb))
        {
            Console.WriteLine("Ошибка, введите именно число");
        }
        return numb;
    }
    static double checkNoZero()
    {
        Console.WriteLine("Введите второе число, отличное от 0");
        double numb;
        while ((!double.TryParse(Console.ReadLine(), out numb) || (numb == 0)))
        {
            Console.WriteLine("Ошибка, введите именно число и убедитесь, что оно не 0!");
        }
        return numb;
    }
    static double function(double x1, double x2)
    {
        double ans = Math.Round(((Math.Pow(Math.Log(x2), 2)) / Math.Cos(x1) - 1), 2);
        return ans;
    }
    static int[] massive(int n)
    {
        Random rand = new Random();
        int[] Array = new int[n];
        int j;
        for (j = 0; j < Array.Length; j++)
        {
            Array[j] = rand.Next(-10, 10);
        }
        return Array;
    }
    static int[] copy(int[] arr)
    {
        int[] newarr = new int[arr.Length];
        for (int index = 0; index < arr.Length; index++)
        {
            newarr[index] = arr[index];
        }
        return newarr;
    }
    static void outputMassive(int[] mass)
    {
        string result = string.Join(',', mass);
        Console.WriteLine((mass.Length <= 10) ? (result) : ("Массивы не могут быть выведены, т.к. их длина больше 10"));
    }
    static void Bubblesort(int[] Arr, int el)
    {
        for (int k = el - 2; k > 0; k--)
        {
            for (int n = 0; n <= k; n++)
            {
                if (Arr[n] > Arr[n + 1])
                {
                    int r = Arr[n];
                    Arr[n] = Arr[n + 1];
                    Arr[n + 1] = r;
                }
            }
        }
    }
    static void shakesort(int[] arr)
    {
        bool swapped = true;
        int start = 0;
        int end = arr.Length - 1;
        while (swapped)
        {
            swapped = false;
            for (int i = start; i < end; i++)
            {
                if (arr[i] > arr[i + 1])
                {
                    int temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                    swapped = true;
                }
            }
            if (!swapped)
                break;
            end--;
            swapped = false;
            for (int i = end - 1; i >= start; i--)
            {
                if (arr[i] > arr[i + 1])
                {
                    int temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                    swapped = true;
                }
            }
            start++;
        }
    }
    static void guess(double trueansver)
    {
        for (int i = 0; i < 3; i++)
        {
            Console.Write("Ваш ответ:");
            double answer = check();
            if (answer == trueansver)
            {
                Console.WriteLine("Правильно, молодец!");
                i = 2;
            }
            else if ((answer != trueansver) & (i < 2))
            {
                Console.WriteLine("Неверно, попробуй ещё раз");
            }
            else if ((answer != trueansver) & (i == 2))
            {
                Console.WriteLine("Неверно, ты проиграл :(");
                Console.WriteLine($"Правильный ответ:{trueansver}");
            }
        }
    }
    static void p1()
    {
        Console.WriteLine("=== Отгадай ответ ===");
        Console.WriteLine("Введите первое число");
        double b = check();
        double c = checkNoZero();
        double trueans = function(b, c);
        Console.WriteLine("Ответьте на вопрос");
        Console.WriteLine("Чему равно значение функции ln^2(b)/cos(a) - 1 , где а и b - введённые вами числа?");
        Console.WriteLine("У вас попыток: 3");
        Console.WriteLine("P.S. Если получилось дробное число, округлите до сотых");
        guess(trueans);
        Console.ReadKey();
    }
    static void p2()
    {
        Console.WriteLine("=== Об авторе ===");
        Console.WriteLine("Горковенко Артём Сергеевич");
        Console.WriteLine("Группа: 6106-090301D");
        Console.ReadKey();
    }
    static void p3()
    {
        Console.WriteLine("=== Сортировка массива ===");
        int elements = InputMassive();
        int[] Arr = massive(elements);
        outputMassive(Arr);
        int[] Arr1 = copy(Arr);
        int[] Arr2 = copy(Arr);
        Stopwatch st = new Stopwatch();
        st.Start();
        Bubblesort(Arr1, elements);
        st.Stop();
        Console.WriteLine("Время сортировки пузырьком:" + st.ElapsedTicks + "мс");
        Stopwatch st2 = new Stopwatch();
        st2.Start();
        shakesort(Arr2);
        st2.Stop();
        Console.WriteLine("Время сортировки перемешиванием:" + st2.ElapsedTicks + "мс");
        outputMassive(Arr1);
        Console.ReadKey();
    }
    static bool exit()
    {
        Console.WriteLine("Уже уходите?");
        Console.WriteLine("Да");
        Console.WriteLine("Нет");
        Console.WriteLine("<Если да - введите 'д' и нажмите Enter>");
        Console.WriteLine("<Если нет - введите 'н' и нажмите Enter>");
        char ex;
        while (!char.TryParse(Console.ReadLine(), out ex) || (ex != 'д' && ex != 'н'))
        {
            Console.WriteLine("Ошибка, введите 'д' или 'н'");
        }
        if (ex == 'д') return true;
        else return false;
    }
    static void Main(string[] args)
    {
        bool en = false;
        while (en == false)
        {
            Console.WriteLine("=== Главное меню ===");
            Console.WriteLine("1. Отгадай ответ");
            Console.WriteLine("2. Об авторе");
            Console.WriteLine("3. Сортировка массива");
            Console.WriteLine("4. Выход");
            Console.WriteLine("<Введите номер нужного пункта и нажмите Enter>");
            int a = check1();
            switch (a)
            {
                case 1:
                    p1();
                    break;
                case 2:
                    p2();
                    break;
                case 3:
                    p3();
                    break;
                case 4:
                    en = exit();
                    break;
            }
        }
    }
}
