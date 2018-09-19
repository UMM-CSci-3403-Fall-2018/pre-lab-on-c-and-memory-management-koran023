# Leak report

There was a leak in the function called strip, where it callocated memory for 'result' and did not free it. However, strip should not be the one to free that memory, since 'result' is returned. The function called is_clean calls strip and assigns the result to a variable called 'cleaned'. This variable is then used in a function call to strcmp, after which it is no longer used. Therefore, the apprpriate code is: `free(cleaned);` after the line `result = strcmp(str, cleaned);` and before `return result == 0;`
