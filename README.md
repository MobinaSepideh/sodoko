# sodoko
using System;

namespace sodoko
{
    class Program
    {
        static void Main(string[] args)
        {
            var sodoko = new char[,]
    {
        { '.', '.', '5', '.', '.', '.', '.', '.', '.' },
        { '.', '.', '.', '.', '.', '1', '8', '.', '.' },
        { '2', '7', '8', '3', '5', '.', '.', '.', '.' },
        { '.', '.', '.', '.', '3', '.', '.', '2', '8' },
        { '.', '6', '.', '.', '4', '.', '.', '1', '.' },
        { '8', '1', '.', '.', '7', '.', '.', '.', '.' },
        { '.', '.', '.', '.', '2', '5', '6', '3', '7' },
        { '.', '.', '3', '7', '.', '.', '.', '.', '.' },
        { '.', '.', '.', '.', '.', '.', '4', '.', '.' }
    };
            solveSodoko(sodoko);
            Console.ReadLine();
        }
        public static void solveSodoko(char[,] sodokoBoard)
        {
            if (sodokoBoard == null || sodokoBoard.Length == 0)
                return;
            resolvent(sodokoBoard);
        }
        private static bool resolvent(char[,] sodokoboard)
        {
            for (int i = 0; i < sodokoboard.GetLength(0); i++)
            {
                for (int j = 0; j < sodokoboard.GetLength(1); j++)
                {
                    if (sodokoboard[i, j] == '.')
                    {
                        for (char c = '1'; c <= '9'; c++)
                        {
                            if (result(sodokoboard, i, j, c))
                            {
                                sodokoboard[i, j] = c;
                                if (resolvent(sodokoboard))
                                    return true;
                                else
                                    sodokoboard[i, j] = '.';
                            }
                        }
                        return false;
                    }
                }
            }
            for (int i = 0; i < sodokoboard.GetLength(0); i++)
            {
                for (int j = 0; j < sodokoboard.GetLength(1); j++)
                {
                    Console.Write(sodokoboard[i, j] + " ");
                }
                Console.Write(Environment.NewLine);
            }
            return true;
        }
        private static bool result(char[,] board, int x, int y, char n)
        {
            for (int i = 0; i < 9; i++)
            {
                if (board[i, y] != '.' && board[i, y] == n)
                    return false;
                if (board[x, i] != '.' && board[x, i] == n)
                    return false;
                if (board[3 * (x / 3) + i / 3, 3 * (y / 3) + i % 3] != '.' && board[3 * (x / 3) + i / 3, 3 * (y / 3) + i % 3] == n)
                    return false;
            }
            return true;
        }
    }
}
