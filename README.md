*This project has been created as part of the 42 curriculum by tchemin.*

# get_next_line

`get_next_line(int fd)` returns the next line read from a file descriptor,
one line per call, including the trailing `\n` when there is one. It returns
`NULL` once the end of file is reached or on error.

Reads are done `BUFFER_SIZE` bytes at a time (default `42`), and the leftover
bytes are kept between calls in a static buffer.

## Files

| File | Content |
|------|---------|
| `get_next_line.c` | the `get_next_line` function |
| `get_next_line_utils.c` | buffer and string helpers |
| `get_next_line.h` | prototypes and the default `BUFFER_SIZE` |

## Usage

```c
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include "get_next_line.h"

int main(void)
{
    int   fd = open("file.txt", O_RDONLY);
    char *line;

    while ((line = get_next_line(fd)))
    {
        printf("%s", line);
        free(line);
    }
    return (0);
}
```

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 main.c get_next_line.c get_next_line_utils.c
```

Each returned line is allocated with `malloc` and must be freed by the caller.
