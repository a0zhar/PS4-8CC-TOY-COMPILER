# PS4-8CC-TOY-COMPILER


### Function for converting arrow functions to regular bracket based C functions
```c
// Example of value to pass as <function_input> is following:
// void helloworld(int arg1, int arg2) => (arg1+arg2);
void convert_arrow_func_to_bracket_func(const char* function_input) {
    // Will contain the bracket version of the function
    char buff[500] = {0};
    
    // Used inside the for-loop to indicate when the => has been found
    int arrowIsFound = 0;
    
    // Current index in the <buff>
    int buf_idx=0;
    
    // Current index in the <function_input>
    int i=0;
    
    // Go Trough <function_input> character by character, until whole
    // function has been converted to an bracket based function
    for (; i < strlen(function_input); i++) {
        // Look for the '=>'
        if (function_input[i] == '=' && function_input[i + 1] == '>') {
            arrowIsFound = 1;
            
            // Skip over the '=>' and any whitespace after it
            i += 2;
            while (function_input[i] == ' ' || function_input[i] == '\t') {
                i++;
            }
            
            // Copy 'return' into the buffer
            strcat(buff, "{ return ");
        }
        // Copy other characters from <function_input> to buff
        if (!arrowIsFound) buff[buf_idx++] = function_input[i];
        
    }
    // Copy the rest of the string after '=>'
    if (arrowIsFound) {
        strcat(buff, &function_input[buf_idx + 2]);
    }
    strcat(buff, " }");
    printf("Converted function: %s\n", buff);
}
```
