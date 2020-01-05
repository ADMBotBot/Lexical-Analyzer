import sys

class Lexer:

  Expr = []
  Filename = ""

  #Tokens
  INT_LIT = 10
  IDENT = 12
  ASSIGN_OP = 20
  ADD_OP = 21
  SUB_OP = 22
  MULT_OP = 23
  DIV_OP = 24
  LEFT_PAREN = 25
  RIGHT_PAREN = 26
  UNKNOWN = 99

  #Reads the file that is given from user, reads each line and passes
  #it to a function for cleaning, and then sends the cleaned string
  #to check for its lexemes and tokens and writes the proper output to a file
  def __init__(self, filename):
    try:
      self.Filename = filename
      with open(filename, 'r') as textfile:
        temp = textfile.readlines()
        self.clean(temp)
        self.Lex_Checker(self.Expr)
      textfile.close()
    except OSError:
      print("Error in opening file")

	#Given a list of lexemes, it finds the token for each lexeme. Upon
  #finding the proper token, both the lexeme and token is appended as
  #a tuple into a new list and is passed for file write. However, if
  #a lexeme is a float, its token is set to unknown. Also, if a
  #variable is alphanumeric, its token is an identity.
  def Lex_Checker(self, expr):
    lexTokenList = []

    def Token_Checker(lex):
      if lex == "(":
        return self.LEFT_PAREN
      elif lex == ")":
        return self.RIGHT_PAREN
      elif lex.isnumeric():
        return self.INT_LIT
      elif lex.isalpha() or lex.isalnum():
        return self.IDENT
      elif lex == "=":
        return self.ASSIGN_OP
      elif lex == "+":
        return self.ADD_OP
      elif lex == "-":
        return self.SUB_OP
      elif lex == "*":
        return self.MULT_OP
      elif lex == "/":
        return self.DIV_OP
      else:
        return self.UNKNOWN

    size = len(expr)
    for i in range(size):
      if len(expr[i]) == 1:
        token = Token_Checker(expr[i])
        lexTokenList.append(tuple((expr[i], token)))
      elif expr[i].isalnum():
        lexTokenList.append(tuple((expr[i], self.IDENT)))
      else:
        token = Token_Checker(expr[i])
        lexTokenList.append(tuple((expr[i], token)))
        self.Lex_Token_Output(lexTokenList)

  #When the file location is passed in the constructor, this function takes
  #that filename and creates an output file with the extension changed. In
  #doing so, it lists the tuple of the lexemes and its token for each expression
  #into the new file.
  def Lex_Token_Output(self, lexTokenList):
    newFilename = []
    size = len(self.Filename)
    for i in range(size):
      if self.Filename[i] != ".":
        newFilename += self.Filename[i]
      else:
        break
    newFilename.append(".lex")
    temp = "".join(newFilename)

    output = open(temp, "w+")
    sizeList = len(lexTokenList)
      for i in range(sizeList):
        if lexTokenList[i][0] != "\n":
          output.write('{l}, {t}\n'.format(l = lexTokenList[i][0], t = lexTokenList[i][1]))
        else:
          output.write("\n")
      output.close()

  #This function cleans the given expression being read from the file. If the
  #given expression contains no spaces, spaces will be added in between lexemes.
  #Once done, the lexemes in the passed in string will be placed in a new list
  #of expressions.
  def clean(self, string):
    size = len(string)
    newList = []

    def add_space(string):
      size = len(string)
      newString = []
      i = 0
      while(i < size):
        tempString = []
        while(string[i].isalnum()):
          tempString.append(string[i])
          i += 1
          newString.append("".join(tempString))
          newString.append("")
          newString.append(string[i])
        return newString
                
    for i in range(size):
      for j in range(size):
        if string[i][j] == "":
          string.replace(string[i], add_space(string[i]))
          break

    for i in range(size):
      expression = string[i]
      sizeExpr = len(expression)
      j = 0
      while j < sizeExpr:
        if expression[j].isalnum() or expression[j] == ".":
          tempString = []
          while expression[j].isalnum() or expression[j] == ".":
            tempString.append(expression[j])
            j += 1
            if j >= sizeExpr:
              break
            newList.append("".join(tempString))
        elif expression[j] != " ":
          newList.append(expression[j])
          j += 1
        else:
          j += 1
          self.Expr = newList

if __name__ == '__main__':
  Lexer(sys.argv[1])
		
#Citation #1: The link showed different ways of handling a file. For this assignment, I had use
#the section of reading from a file line by line and also how to write to a new file
#in the constructor.
#(Link: https://www.guru99.com/reading-and-writing-files-in-python.html#4)

#Citation #2: The link explains the use of isalpha(). This was used in the code by determining if
#the lexeme is a legal variable or not.
#(Link: https://www.geeksforgeeks.org/python-string-isalpha-application/)

#Citation #3: The link provides info on isnumeric(). As with isalpha(), this was used in the code
#to determine if the lexeme is an integer literal.
#(Link: https://www.tutorialspoint.com/python/string_isnumeric.htm)

#Citation #4: The link privded gives info on the replace function. This was used to in the code to
#replace an element in the string through a function.
#(Link: https://www.geeksforgeeks.org/python-string-replace/)

#Citation #5: The link gives info on what alnum does. It was used in the code to check if the lexeme
#was a combination of alphanumerics.
#			  (Link: https://www.programiz.com/python-programming/methods/string/isalnum)
