# Recount
/*Maycoll, Ben, Jonathan, Diego
 *Figuring out the Recount Kattis problem
 * 4/23/2022 - We mainly spoke about it amongst each other within our group calls and several other forms of communication.
 */


using System;
using System.Collections.Generic;
using System.Text;

namespace RecountKP
{
	class Program
	{
		static void Main(string[] args)
		{

            Dictionary<string, int> runningcandt = new Dictionary<string, int>();
            string name; //Connects all the names to this string which is also included in the Dictionary
            int x, maxCount = 0, countOfMaxCount = 0;
            string canditateName = "";
            int count = 0;

            do
            {
                name = Console.ReadLine();
                if (name == "***")
                    break;
                if (name.Trim().Equals(""))
                    continue;

                for (x = 0; x < name.Length; x++)
                    if (name[x] != '-' && name[x] != ' ' && Char.IsLetterOrDigit(name, x) == false)
                        break;


                if (x != name.Length)
                {
                    //What this does is that it should show that the name is (Invalid;)
                    continue;
                }
                count++;
                if (runningcandt.ContainsKey(name))
                {
                    runningcandt[name] += 1;

                    if (runningcandt[name] > maxCount)
                    {
                        canditateName = name;
                        maxCount = runningcandt[name];
                        countOfMaxCount = 1;
                    }
                    else if (runningcandt[name] == maxCount)
                        countOfMaxCount += 1;
                }
                else  
                {
                    if (maxCount == 0)
                    {
                        canditateName = name;
                        maxCount = 1;
                        countOfMaxCount = 1;
                    }
                    runningcandt.Add(name, 1);
                    if (maxCount == 1)
                        countOfMaxCount += 1;

                }
            } while (name != "***"); //Stops reading once *** is read.


            if (count <= 1 || countOfMaxCount > 1)
                Console.WriteLine("Runoff!"); // Result for when there is not a single majority
            else
                Console.WriteLine(canditateName); //Results if there is a majority.
            
		}
	}
}
