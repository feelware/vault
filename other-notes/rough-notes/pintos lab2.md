### current stack (`setup_stack`)

| description          | data | start      | end | size (bytes) | owner  |
| -------------------- | ---- | ---------- | --- | ------------ | ------ |
| `PHYS_BASE`          |      | 0xc0000000 |     |              | kernel |
| ...rest of the stack |      |            |     |              |        |
`esp`: 0xc0000000

### expected stack

| description                                     | data       | start      | end        | size (bytes) | owner   |
| ----------------------------------------------- | ---------- | ---------- | ---------- | ------------ | ------- |
| `PHYS_BASE`                                     |            | 0xc0000000 |            |              | kernel  |
| contents of the string that `argv[0]` points to | echo\0     | 0xbffffffb | 0xbfffffff | 5            | process |
| contents of the string that `argv[1]` points to | hola\0     | 0xbffffff6 | 0xbffffffa | 5            | process |
| 4-byte-word align padding                       | 0x0000     | 0xbffffff4 | 0xbffffff5 | 2            | process |
| `argv[2]` (null pointer sentinel)               | 0x00000000 | 0xbffffff0 | 0xbffffff3 | 4            | process |
| `argv[1]`                                       | 0xbffffffb | 0xbfffffec | 0xbfffffef | 4            | process |
| `argv[0]`                                       | 0xbffffff6 | 0xbfffffe8 | 0xbfffffeb | 4            | process |
| `argv` (pointer to `argv[0]`)                   | 0xbfffffe8 | 0xbfffffe4 | 0xbfffffe7 | 4            | process |
| `argc`                                          | 0x00000002 | 0xbfffffe0 | 0xbfffffe3 | 4            | process |
| fake return address (`esp` must point here)     | 0x00000000 | 0xbfffffdc | 0xbfffffdf | 4            | process |
| ...rest of the stack                            |            |            |            |              |         |
`esp`: 0xbfffffdc
