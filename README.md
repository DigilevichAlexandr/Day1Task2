using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ASP.NET.Digilevich.Day1.Task3
{
    class SortClass
    {
        public static void SortLinesKind(int[][] arr,int k)
        {
            QuickSortKind(arr,0,1,ref k);
        }


        static int Partition(int[][] numbers, int left, int right,ref int k)
        {          
            if (k % 2==1)
            {
                int pivot = SortClass.FindKind(numbers[left], k);
                while (true)
                {
                    while (SortClass.FindKind(numbers[left], k) < pivot)
                        left++;
                    while (SortClass.FindKind(numbers[right], k) > pivot)
                        right--;
                    if (SortClass.FindKind(numbers[right], k) == pivot && SortClass.FindKind(numbers[left], k) == pivot)
                    {
                        left++;
                    }
                    if (left < right)
                    {
                        int[] temp = numbers[right];
                        numbers[right] = numbers[left];
                        numbers[left] = temp;
                    }
                    else
                    {
                        return right;
                    }
                }            
            }
            else
            {
                int pivot = SortClass.FindKind(numbers[left], k);
                while (true)
                {
                    while (SortClass.FindKind(numbers[left], k) > pivot)
                        left++;
                    while (SortClass.FindKind(numbers[right], k) < pivot)
                        right--;
                    if (SortClass.FindKind(numbers[right], k) == pivot && SortClass.FindKind(numbers[left], k) == pivot)
                    {
                        left++;
                    }
                    if (left < right)
                    {
                        int[] temp = numbers[right];
                        numbers[right] = numbers[left];
                        numbers[left] = temp;
                    }
                    else
                    {
                        return right;
                    }
                } 
            }

        }

        /// <summary>
        /// 1 - в порядке возрастания(убывания) максимальных элементов строк матрицы;
        /// 2 - в порядке возрастания(убывания) минимальных элементов строк матрицы;
        /// 3 - в порядке возрастания(убывания)  сумм элементов строк матрицы.
        /// </summary>
        /// <param name="arr"></param>
        /// <param name="kind"></param>
        /// 
        static void QuickSortKind(int[][] arr, int left, int right,ref int k)
        {
            if (left < right)
            {
                int pivot = Partition(arr, left, right,ref k);
                if (pivot > 1)
                    QuickSortKind(arr, left, pivot - 1,ref k);

                if (pivot + 1 < right)
                    QuickSortKind(arr, pivot + 1, right,ref k);
            }

        }        
        
        private static int FindKind(int[] arr,int k)
        {
            int val = 0;
            if (k ==1 || k==2)
            {
                int max = arr[0];
                        for (int i = 1; i < arr.Length; i++)
                            if (arr[i] > max)
                                max = arr[i];
                        val = max;
            }
            else      
                if (k == 3 || k== 4)
                    {
                        int min = arr[0];
                        for (int i = 1; i < arr.Length; i++)
                            if (arr[i] < min)
                                min = arr[i];
                        val = min;
                    }
                else
                    if (k ==5 || k==6)
                    {
                        int sum = 0;
                        for (int i = 1; i < arr.Length; i++)
                            sum += arr[i];
                        val = sum;
                    }
            return val;            
        }
    }
}
