using System;

namespace NewBigCalculator
{

    public class TheFirstNumber
    {
        public string num_1 = Console.ReadLine();

        // ввод числа

        public int[] func1()
        {
          
          int TheFirstLength = num_1.Length;

          char[] array1 = new char[TheFirstLength];
          int[] digits_1 = new int[TheFirstLength];

        // перевод из строки в массив чисел

            for (int i = 0; i < TheFirstLength; i++)
            {
                array1[i] = num_1[i];
            }

            for (int i = 0; i < TheFirstLength; i++)
            {
                digits_1[i] = Convert.ToInt32(Char.GetNumericValue(array1[i]));
            }

            /*for (int i = 0; i < TheFirstLength; i++)
            {
               Console.Write(digits_1[i]);
            }*/

            return digits_1;
        }
    }

    public class TheSecondNumber
    {
        public string num_2 = Console.ReadLine();
        
        //ввод числа

        public int[] func2() 
        {         
          int TheSecondLength = num_2.Length;

          char[] array2 = new char[TheSecondLength];
          int[] digits_2 = new int[TheSecondLength];

        // перевод из строки в массив чисел

             for (int i = 0; i < TheSecondLength; i++)
             {
                array2[i] = num_2[i];
             }
             for (int i = 0; i < TheSecondLength; i++)
             {
                digits_2[i] = Convert.ToInt32(Char.GetNumericValue(array2[i]));
             }
             /*for (int i = 0; i < TheSecondLength; i++)
             {
                Console.Write(digits_2[i]);
             }*/

            return digits_2;
        }
    }

        class Program
        {
            static void Main(string[] args)
            {           
                TheFirstNumber number1 = new TheFirstNumber();                           
                TheSecondNumber number2 = new TheSecondNumber();
                
                        int[] digit1 = number1.func1(); //вызов массива первого числа
                        int[] digit2 = number2.func2(); //вызов массива второго числа


                        int TheFirstLength = digit1.Length;
                        int TheSecondLength = digit2.Length;

             
                    int[] reverse1 = new int[TheFirstLength];
                    int[] reverse2 = new int[TheSecondLength];


                        int max = TheFirstLength;
                        int min = TheSecondLength;


            //проверка какое число длиннее

            if(TheSecondLength > max)
            {
                max = TheSecondLength;
                min = TheFirstLength;
            }

            int[] summ = new int[max];
            int[] diff = new int[max];

                int j1 = TheFirstLength - 1;
                int j2 = TheSecondLength - 1;

            bool try_diff = false;


                    //запись чисел наоборот

                        for (int i = 0;i < TheFirstLength;i++)
                        {               
                            reverse1[i] = digit1[j1];
                            j1--;
                        }

                        for(int i = 0;i < TheSecondLength; i++)
                        {
                            reverse2[i] = digit2[j2];
                            j2--;
                        }


                    //вычисление разности если первое число больше второго

            if(max == TheFirstLength && TheFirstLength != TheSecondLength)
            {
                int i = 0;
                    
                while(i < TheFirstLength)
                {
                    if (i < TheSecondLength)
                    {
                        if(try_diff == true)
                        {
                            reverse1[i]--;
                            try_diff = false;
                        }

                        if (reverse1[i] >= reverse2[i])
                        {
                            diff[i] = reverse1[i] - reverse2[i];
                        }
               
                        if (reverse1[i] < reverse2[i])
                        {
                            int j = i;
                            while(reverse1[j] == 0)
                            {                                                                
                                if (reverse2[j] > 0)
                                {
                                    reverse1[j] += 10;
                                }                                                               
                                j++;                                  
                            }
                            diff[i] = reverse1[i] - reverse2[i];
                        }
                        i++;                        
                    }
                    else
                    {                        
                        diff[i] = Math.Abs(reverse1[i]);
                        i++;
                        if (try_diff == true)
                        {
                            diff[i - 1]--;
                            try_diff = false;
                        }
                    }
                                                                
                }
            }

            //вычисление разности если длина первого равна длине второго

            

            if(TheFirstLength == TheSecondLength)
            {
                int i = 0;
                while(i < max)
                {
                    if (i < max - 1)
                    {
                        if(try_diff == true)
                        {
                            diff[i]--;
                            try_diff = false;
                        }

                        if (reverse1[i] > reverse2[i])
                        {
                            diff[i] = reverse1[i] - reverse2[i];
                        }
                        if(reverse1[i] == reverse2[i])
                        {
                            diff[i] = 0;
                        }
                        if(reverse1[i] < reverse2[i])
                        {
                            diff[i] = Math.Abs((reverse1[i] + 10) - reverse2[i]);
                            try_diff = true;      
                        }
                        i++;
                    }
                    else
                    {
                        if(i == max - 1)
                        {
                            diff[i] = reverse1[i] - reverse2[i];                          
                            if(try_diff == true)
                            {
                                diff[i] = diff[i] - 1;
                                try_diff = false;
                            }
                            i++;
                        }

                    }                                         
                }
            }



            for(int i = max - 1; i > -1; i --)
            {
                Console.Write(diff[i]);
            }



            /*     //вычисление суммы если первое число длиннее второго

             if (max == TheFirstLength && TheFirstLength != TheSecondLength)
             {
                 int i = 0;

                 while (i < TheFirstLength)
                 {
                     if (i < TheSecondLength)
                     {
                         summ[i] = reverse1[i] + reverse2[i];

                         if (i > 0)
                         {

                             if (summ[i - 1] >= 10)
                             {
                                 int temp;
                                 temp = summ[i - 1] % 10;
                                 summ[i - 1] = temp;
                                 summ[i] = summ[i] + 1;
                             }
                         }
                         i++;
                     }
                     else
                     {
                         summ[i] = reverse1[i];

                         if (i > 0)
                         {
                             if (summ[i - 1] >= 10)
                             {
                                 int temp;
                                 temp = summ[i - 1] % 10;
                                 summ[i - 1] = temp;
                                 summ[i] = summ[i] + 1;
                             }
                         }
                         i++;
                     }
                 }
             }


             //вычисление суммы если второе число длиннее первого

             if (max == TheSecondLength && TheSecondLength != TheFirstLength)
             {
                 int i = 0;

                 while(i < TheSecondLength)
                 {
                     if(i < TheFirstLength)
                     {
                         summ[i] = reverse1[i] + reverse2[i];

                         if (i > 0)
                         {
                             if (summ[i - 1] >= 10)
                             {
                                 int temp;
                                 temp = summ[i - 1] % 10;
                                 summ[i - 1] = temp;
                                 summ[i] = summ[i] + 1;
                             }                            
                         }
                         i++;
                     }
                     else
                     {
                         summ[i] = reverse2[i];

                         if (i > 0)
                         {
                             if (summ[i - 1] >= 10)
                             {
                                 int temp;
                                 temp = summ[i - 1] % 10;
                                 summ[i - 1] = temp;
                                 summ[i] = summ[i] + 1;
                             }
                         }
                         i++;
                     }
                 }
             }


                 //вычисление суммы если числа одинковой длины

             if (TheFirstLength == TheSecondLength)
             {
                 int i = 0;

                 while (i < max)
                 {
                     summ[i] = reverse1[i] + reverse2[i];

                     if (i > 0)
                     {
                         if (summ[i - 1] >= 10)
                         {
                             int temp;
                             temp = summ[i - 1] % 10;
                             summ[i - 1] = temp;
                             summ[i] = summ[i] + 1;
                         }
                     }
                     i++;
                 }
             }


             //вывод суммы

             Console.WriteLine();
             Console.WriteLine("Сумма равна: \n");

             for (int i = max - 1;i > -1; i--)
                 {
                     Console.Write(summ[i]);
                 }
             Console.WriteLine();

                         */


            //разность

        }
        }
}
