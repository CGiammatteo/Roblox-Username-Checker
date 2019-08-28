using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Text;
using System.Threading.Tasks;
using Newtonsoft.Json;

using System.IO;

namespace Username_Checker
{
    class Program
    {
        static void Main(string[] args)
        {
            string letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789abcdefghijklmnopqrstuvwxyz1234567890";

            List<string> Unused = new List<string>()
            { };



            Console.Title = "Username Checker - Created By Gostrondude";

            Console.Write("Type 1 Check Usernames, Or Type 2 To Generate **WORKING** Usernames: ");
            string choice = Console.ReadLine();
            if (choice == "1")
            {

                Console.WriteLine("Grabbing Usernames From " + System.AppContext.BaseDirectory + @"Usernames.txt");

                string Contents = "";

                using (var Stream = new FileStream(System.AppContext.BaseDirectory + @"Usernames.txt", FileMode.Open, FileAccess.Read))
                using (var ReadFile = new StreamReader(Stream, Encoding.Default))
                {
                    Contents = ReadFile.ReadToEnd();
                }
                Console.ForegroundColor = ConsoleColor.Green;
                Console.WriteLine("Grabbed Usernames Successfully!");
                Console.ForegroundColor = ConsoleColor.White;
                Console.WriteLine("Starting...");
                WebClient wc = new WebClient();

                string[] Current = Contents.Split(new[] { Environment.NewLine }, StringSplitOptions.None);

                foreach (string Cur in Current)
                {
                    dynamic json = JsonConvert.DeserializeObject(wc.DownloadString(string.Format("https://auth.roblox.com/v2/usernames/validate?request.username={0}&request.birthday=04%2F15%2F02&request.context=Signup", Cur)));

                    if (json.message == "Username is already in use")
                    {
                        Console.ForegroundColor = ConsoleColor.Red;
                        Console.WriteLine(Cur + " Is Already Taken!");
                        Console.ForegroundColor = ConsoleColor.White;
                    }
                    else if (json.message == "Username is valid")
                    {
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine(Cur + " Is Not Taken!");
                        Console.ForegroundColor = ConsoleColor.White;
                        Unused.Add(Cur);

                    }
                }

                using (System.IO.StreamWriter file =
            new System.IO.StreamWriter(System.AppContext.BaseDirectory + @"Unused.txt"))
                {
                    foreach (string name in Unused)
                    {
                        file.WriteLine(name);
                    }
                }
                wc.Dispose();
                Console.WriteLine("Web Client Successfuly Disposed!");



                Console.Write("Checking Compleated Successfully! \nPress Any Key To Exit...");
                Console.ReadKey();
            }

            else if (choice == "2")
            {
                WebClient wc = new WebClient();
                Random r = new Random();
                Console.Write("How Many Characters Would You Like In The Usernames?: ");
                int thing = Convert.ToInt32(Console.ReadLine());

                Console.Write("How Many Usernames Would You Like To Generate?: ");
                int num = Convert.ToInt32(Console.ReadLine());

                int Correct = 0;

                while (Correct < num)
                {

                    string A = new string(letters.Select(c => letters[r.Next(letters.Length)]).Take(thing).ToArray());

                    dynamic json = JsonConvert.DeserializeObject(wc.DownloadString(string.Format("https://auth.roblox.com/v2/usernames/validate?request.username={0}&request.birthday=04%2F15%2F02&request.context=Signup", A.ToString())));

                    if (json.message == "Username is already in use")
                    {
                        Console.ForegroundColor = ConsoleColor.Red;
                        Console.WriteLine(A.ToString() + " Is Already Taken!");
                        Console.ForegroundColor = ConsoleColor.White;
                    }
                    else if (json.message == "Username is valid")
                    {
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine("Generated Username: " + A.ToString() + " Successfully!");
                        Console.ForegroundColor = ConsoleColor.White;
                        Unused.Add(A.ToString());
                        Correct = Correct + 1;

                        Console.Title = "Username Checker - Created By Gostrondude [" + Correct + "/" + num + "]";

                    }
                }
                wc.Dispose();
            }

         
                using (System.IO.StreamWriter file =
                    new System.IO.StreamWriter(System.AppContext.BaseDirectory + @"Unused.txt"))
                {
                    foreach (string name in Unused)
                    {
                        file.WriteLine(name);
                    }
                }
               

                Console.Write("Username Generation Completed! \nPress Any Key To Exit...");
                Console.ReadKey();
            }


        }
    
    
    }
