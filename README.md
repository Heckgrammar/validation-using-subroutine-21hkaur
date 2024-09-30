![image](https://github.com/user-attachments/assets/a0b510e2-4b5c-4270-b99d-626289e14df0)
Keeps asking me to enter password

![image](https://github.com/user-attachments/assets/9e105fc0-662c-46b9-b6ce-ad2dfd999d0c)
Won't let me run my code:
![image](https://github.com/user-attachments/assets/cbd0b1dd-44a7-4946-9c4d-199e79ac6e6a)


![image](https://github.com/user-attachments/assets/b2b6a885-dd90-4865-a62a-96bb8e174a54)
My Code:
    
    static void Main(string[] args)
    {
        string firstName, lastName, username, password, emailAddress;
        int age;

        // get the user inputs until all are valid.
        // The username should only be output once
        Console.Write("Enter first name: ");
        firstName = Console.ReadLine();
        Console.Write("Enter last name: ");
        lastName = Console.ReadLine();
        bool isName = ValidName(firstName, lastName);
       
        Console.Write("Enter age: ");
        age = Convert.ToInt32(Console.ReadLine());
        bool isAge = validAge(age);
        
        Console.Write("Enter Password: ");
        password = Console.ReadLine();
        bool isPass = ValidPassword(password);
       
        Console.Write("Enter email address: ");
        emailAddress = Console.ReadLine();
        bool isEmail = validEmail(emailAddress);


        while (isName == false)
        {
            Console.WriteLine("Both names must contain atleast 2 letters, and all characters MUST be letters: ");
            Console.Write("Enter first name: ");
            firstName = Console.ReadLine();
            Console.Write("Enter last name: ");
            lastName = Console.ReadLine();
            isName = ValidName(firstName, lastName);
        }

        while (isAge == false)
        {
            Console.WriteLine("Age must be between 11 and 18 inclusive: ");
            Console.Write("Re-enter age: ");
            age = Convert.ToInt32(Console.ReadLine());
            isAge = validAge(age);
        }

        while (isPass == false)
        {
            Console.WriteLine("Password must be atleast 8 characters in length, must contain a mix of lower case, upper case, symbols and numbers and must not contain more than 2 consecutive repeating letters or numbers: ");
            Console.Write("Re-enter Password: ");
            password = Console.ReadLine();
            isPass = ValidPassword(password);
        }

        while (isEmail == false)
        {
            Console.WriteLine("Email must have atleast 2 characters followed by a @ symbol, at least 2 characters followed by a ., at least 2 characters after the., must countain only one @ and must not contain any other non letter or number characters: ");
            Console.Write("Re-enter email address: ");
            emailAddress = Console.ReadLine();
            isEmail = validEmail(emailAddress);
        }

        username = createUserName(firstName,lastName,age);
        Console.WriteLine($"Username is {username}, you have successfully registered please remember your password");

        //  Test your program with a range of tests to show all validation works
        // Show your evidence in the Readme

    }
    static bool ValidName(string name1, string name2)
    {
        int len1 = name1.Length;
        int len2 = name2.Length;
        string fullName = name1 + name2;
        bool isLetters = fullName.All(Char.IsLetter);
        if (len1 >= 2 && len2 >= 2 && isLetters)
        {
            return true;
        }
        return false;
        // name must be at least two characters and contain only letters
    }

    static bool validAge(int age)
    {
        if (age >= 11 && age <= 18)
        {
            return true;
        }
        return false;
        //age must be between 11 and 18 inclusive
    }

   
    static bool ValidPassword(string password)
    {
        int length = password.Length;
        if (length > 8)
        {
            return false;
           
        }
        return false;
        // Check password is at least 8 characters in length

        bool upperCase = password.Any(char.IsUpper);
        bool lowerCase = password.Any(char.IsLower);
        bool number = password.Any(char.IsDigit);
        bool symbol = password.Any(char.IsSymbol);
        if (!upperCase || !lowerCase || !number || !symbol)
        {
            return false;
        }
        // Check password contains a mix of lower case, upper case and non letter characters
        // QWErty%^& = valid
        // QWERTYUi = not valid
        // ab£$%^&* = not valid
        // QWERTYu! = valid

        for (int i = 0; i < length - 2; i++)
        {
            if (password[i] == password[i + 1] && password[i] == password[i + 2])
            {
                return false;
            }
        }
        // Check password contains no runs of more than 2 consecutive or repeating letters or numbers
        // AAbbdd!2 = valid (only 2 consecutive letters A and B and only 2 repeating of each)
        // abC461*+ = not valid (abC are 3 consecutive letters)
        // 987poiq! = not valid (987 are consecutive)


    }
    static bool validEmail(string email)
    {
        int length = email.Length;
        bool hasNumbers = email.Any(char.IsDigit);
        if (email.IndexOf('@') >= 3)
        {
            if (email.IndexOf('.') >= email.IndexOf('@') + 3)
            {
                if (length >= email.IndexOf('.') + 2)
                {
                    if (!hasNumbers)
                    {
                        return true;
                    }
                }
            }
        }
        return false;
        // a valid email address
        // has at least 2 characters followed by an @ symbol
        // has at least 2 characters followed by a .
        // has at least 2 characters after the .
        /// contains only one @ and any number of .
        /// does not contain any other non letter or number characters

    }
    static string createUserName(string firstName, string lastName, int age)
    {
        char one = firstName[0];
        string one1 = Convert.ToString(one);
        char two = firstName[1]; ///OR JUST DO SUBSTRINGS
        int lastLen = lastName.Length - 1;
        char three = lastName[lastLen];
        char four = lastName[lastLen - 1];
        string five = Convert.ToString(age);
        string userName = one1 + two + three + four + five;
        return userName;
        // username is made up from:
        // first two characters of first name
        // last two characters of last name
        // age
        //e.g. Bob Smith aged 34 would have the username Both34
    }

}
