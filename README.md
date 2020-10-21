def nToDecimal(before_dec, base, after_dec):
    digit_pos = 0
    new_num1 = 0
    i = len(before_dec) -1
    
    for digit_pos in range(len(before_dec)):
        if before_dec[i] == 'A':
            digit_val = 10
        elif before_dec[i] == 'B':
            digit_val = 11
        elif before_dec[i] == 'C':
            digit_val = 12
        elif before_dec[i] == 'D':
            digit_val = 13
        elif before_dec[i] == 'E':
            digit_val = 14
        elif before_dec[i] == 'F':
            digit_val = 15
        else:
            digit_val =int(before_dec[i])
            
        new_num1 += digit_val * (base ** digit_pos)
        i -= 1
    new_num = new_num1
    
    if after_dec != '':
        new_num2 = 0
        #digit_pos = 2
        for digit_pos in range(len(after_dec) - 1):
            if after_dec[digit_pos +1] == 'A':
                digit_val = 10
            elif after_dec[digit_pos +1] == 'B':
                digit_val = 11
            elif after_dec[digit_pos +1] == 'C':
                digit_val = 12
            elif after_dec[digit_pos +1] == 'D':
                digit_val = 13
            elif after_dec[digit_pos +1] == 'E':
                digit_val = 14
            elif after_dec[digit_pos +1] == 'F':
                digit_val = 15
            else:
                digit_val = int(after_dec[digit_pos +1])
                
            new_num2 += digit_val * (base ** -(digit_pos+1))
            
        new_num = new_num1 + new_num2
    
        
    return new_num

#*****************************************************************************
    
def decimalTobase_n(before_dec, base, after_dec):
    before_dec = int(before_dec)     #point er ager part
    res = 1
    new_num1 = ''
#---------- point er ager part er kaj--------------
    while(res != 0):
        res = before_dec // base
        rem = before_dec % base
        if rem == 10:
            new_num1 += 'A'
        elif rem == 11:
            new_num1 += 'B'
        elif rem == 12:
            new_num1 += 'C'
        elif rem == 13:
            new_num1 += 'D'
        elif rem == 14:
            new_num1 += 'E'
        elif rem == 15:
            new_num1 += 'F'
        else:
            new_num1 += str(rem)
            
        before_dec = res
        
    new_num1 = new_num1[::-1]     #MSB LSB wise reverse kora
    new_num = new_num1
    
#--------- point er porer kaj ---------
    
    if after_dec != '':
        new_num2 = ''
        num = "123456789'11''12''13''14''15'"
        i = 0
        while(after_dec[0] not in num or after_dec[2] != '0'):
            if  after_dec[0] in num:
                if after_dec[1] == ".":                        #point er age 2 ghor hole
                    after_dec = '0' + after_dec[1::]           #2 ta jog krbe otherwise 1 ta.
                else:
                    after_dec = '0' + after_dec[2::]
            after_dec = str(float(after_dec) *base)
            if after_dec[1] == '.':
                temp = after_dec[0]
            else:
                temp = after_dec[0] +after_dec[1]
                
            temp = int(temp)
            if temp == 10:
                new_num2 += 'A'
            elif temp == 11:
                new_num2 += 'B'
            elif temp == 12:
                new_num2 += 'C'
            elif temp == 13:
                new_num2 += 'D'
            elif temp == 14:
                new_num2 += 'E'
            elif temp == 15:
                new_num2 += 'F'
            else:
                new_num2 += str(temp)
            
            i += 1
            if i > 20:
                break
        new_num = new_num1 + '.' + new_num2
        
    
    return new_num

#****************************************************************************
    
given_num = input("Enter a number: ")
given_num_base = int(input("Enter the given number base: "))
expected_num_base = int(input("Enter the expected number base: "))

if '.' in given_num:
    before_dec, after_dec = given_num.split('.')
    after_dec = '.' + after_dec
else:
    before_dec = given_num
    after_dec = ''

print("Your expected number is:",end =' ')  

if given_num_base == 10:
    print(decimalTobase_n(before_dec, expected_num_base, after_dec))

elif expected_num_base == 10:
    print(nToDecimal(before_dec, given_num_base, after_dec))
    
else:
    decimal_num = nToDecimal(before_dec, given_num_base, after_dec)
    decimal_num = str(decimal_num)
    if '.' in decimal_num:
        before_dec, after_dec = decimal_num.split('.')
        after_dec = '.' + after_dec
    else:
        before_dec = decimal_num
        after_dec = ''
     
    print(decimalTobase_n(before_dec, expected_num_base, after_dec))
    
