using System;

namespace NetLab1
{
   class Quadrilatera
    {
       public double PointAx ;
       public double PointAy ;
       public double PointBx;
       public double PointBy;
       public double PointDx;
       public double PointDy;
       public double PointCx;
       public double PointCy;
        public Quadrilatera()
        {
        }
       public double AB()
        {return Math.Sqrt((Math.Pow(this.PointBx - this.PointAx, 2)) + (Math.Pow(this.PointBy - this.PointAy, 2)));

        }
        public double BC()
        {
            return Math.Sqrt((Math.Pow(this.PointCx - this.PointBx, 2)) + (Math.Pow(this.PointCy - this.PointBy, 2)));
        }
        public double AD()
        {
            return Math.Sqrt((Math.Pow(this.PointDx - this.PointAx, 2)) + (Math.Pow(this.PointDy - this.PointAy, 2)));
        }
        public double CD()
        {
            return Math.Sqrt((Math.Pow(this.PointDx - this.PointCx, 2)) + (Math.Pow(this.PointDy - this.PointCy, 2)));
        }
        public bool IsQuadrilateral()

        {
            bool result = false;
            if (
                (this.AB() + this.BC() + this.AD() > this.CD()) &&
                (this.AB() + this.BC() + this.CD() > this.AD()) &&
                (this.AB() + this.CD() + this.AD() > this.BC()) &&
                (this.CD() + this.BC() + this.AD() > this.AB()) &&
                (this.GetDiagonal1() > 0) &&
                (this.GetDiagonal2() > 0)
                )
                result = true;

            return result;
        }
        public double GetPerimeter()
        {
            return AB() + BC() + AD() + CD();
        }
        public double GetSquare()
        {
            return 0.5 * Math.Abs((PointAx - PointBx) * (PointAy + PointBy) + (PointBx - PointCx) * (PointBy + PointCy) + (PointCx - PointDx) * (PointCy + PointDy) + (PointDx - PointAx) * (PointDy + PointAy));
        }
        public double GetDiagonal1()
        {
            return Math.Sqrt((Math.Pow(CD(), 2) + AD() + BC()) - ((AD() * Math.Pow(CD(), 2) - Math.Pow(AB(), 2)) / (AD() - BC())));

        }
        public double GetDiagonal2()
        {
            return Math.Sqrt((Math.Pow(AB(), 2) + AD() + BC()) - ((AD() * Math.Pow(AB(), 2) - Math.Pow(CD(), 2)) / (AD() - BC())));
        }
        public void PrintInfo()
        {
            Console.WriteLine(this.IsQuadrilateral() ? "Quadrilateral" : "NOT Quadrilateral");
            Console.WriteLine("side AB = "+ this.AB());
            Console.WriteLine("side BC = "+ this.BC());
            Console.WriteLine("side AD = "+ this.AD());
            Console.WriteLine("side CD = "+ this.CD());
            Console.WriteLine("Perimeter = " + this.GetPerimeter());
            Console.WriteLine("Square = " + this.GetSquare());
            Console.WriteLine("Diagonal AC = " + this.GetDiagonal1());
            Console.WriteLine("Diagonal BD = " + this.GetDiagonal2());
            Console.WriteLine(" ________________________________________________\n");
        }
    }
    class Square : Quadrilatera
    {
        
        public double GetSPerimeter()
        {
            return this.AB() * 4;

        }
        public double GetSSquare()
        {
            return this.AB() * this.AB();

        }
        public bool IsSquare()

        {
            bool result = false;
            if (this.AB() > 0)
                result = true;
                return result;
            
        }
        public double  GetSDiagonal()
        {
            return 2*(Math.Sqrt(this.AB()));
        }
        public void PrintInfoS()
        {
            Console.WriteLine(this.IsSquare() ? "Square" : "NOT Square");
            Console.WriteLine("SIDE = " + this.AB());
            Console.WriteLine("Square Perimeter = " + this.GetSPerimeter());
            Console.WriteLine("Square of Square ^_^ = " + this.GetSSquare());
            Console.WriteLine("Square Diagonal  = " + this.GetSDiagonal());
            Console.WriteLine(" ________________________________________________\n");
        }

    }
    class Program
    {
        static void Main(string[] args)
        {
            double min=9999;double max=-9999;
            int x; string N;int y;string M;
            Console.WriteLine("Enter The Number of Quadrilaterals ");
            N = Console.ReadLine();
            x = Convert.ToInt32(N);
            Random r = new Random();
            Quadrilatera Q1 = new Quadrilatera();
            if (x <= 0)
                Console.WriteLine("ERROR TRY AGAIN");
            for (int i = 0; i < x; i++)
            {
               
                Q1.PointAx = r.NextDouble() * 10;
                Q1.PointAy = r.NextDouble() * 10;
                Q1.PointBx = r.NextDouble() * 10;
                Q1.PointBy = r.NextDouble() * 10;
                Q1.PointCx = r.NextDouble() * 10;
                Q1.PointCy = r.NextDouble() * 10;
                Q1.PointDx = r.NextDouble() * 10;
                Q1.PointDy = r.NextDouble() * 10;
                Q1.PrintInfo();
                if (Q1.GetSquare() < min) 
                        
                {
                    min = Q1.GetSquare();
                }
                if (Q1.GetSquare() > max)
                {
                    max= Q1.GetSquare();
                }

            }
            Console.WriteLine("The Biggest Square of Quadrilaterals is " + max);
            Console.WriteLine("The Smallest Square of Quadrilaterals is " + min);
            Console.WriteLine(" ________________________________________________\n");
            Console.WriteLine("Enter The Number of Squares ");
            M = Console.ReadLine();
            y = Convert.ToInt32(M);
            Console.WriteLine("\n");
            Square S = new Square();
            if (y <= 0)
                Console.WriteLine("ERROR TRY AGAIN");
            for (int i = 0; i < y; i++)
            {
                S.PointAx = r.NextDouble()*10;
                S.PointAy = r.NextDouble()*10;
                S.PointBx = r.NextDouble()*10;
                S.PointBy = r.NextDouble()*10;
                S.PrintInfoS();
            }
           
            Console.ReadKey();

        }
        
    }
}
/*public bool IsSquare()

{
    bool result = false;
    if ((this.AB() > 0)&
        (AB() == BC())&
        (BC() == CD()) &                   ПРОВЕРКА СУЩЕСТВОВАНИЯ КВАДРАТА ПРИ ЗАПОЛНЕНИИ С КЛАВИАТУРЫ ИЛИ ПРИ ЗАДАННЫХ КООРДИНАТАХ
        (AB() == CD()) 
        )
        result = true;
    return result;

}*.
