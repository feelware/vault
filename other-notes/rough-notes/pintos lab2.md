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
| contents of the string that `argv[1]` points to | bar\0      | 0xbffffffc | 0xbfffffff | 4            | process |
| contents of the string that `argv[0]` points to | fu\0       | 0xbffffff9 | 0xbffffffb | 3            | process |
| 4-byte-word align padding                       | 0          | 0xbffffffa | 0xbffffffa | 1            | process |
| `argv[2]` (null pointer sentinel)               | 0          | 0xbffffff6 | 0xbffffff9 | 4            | process |
| `argv[1]`                                       | 0xbffffffc | 0xbffffff2 | 0xbffffff5 | 4            | process |
| `argv[0]`                                       | 0xbffffff9 | 0xbfffffed | 0xbffffff1 | 4            | process |
| `argv` (pointer to `argv[0]`)                   | 0xbfffffed | 0xbfffffe9 | 0xbfffffec | 4            | process |
| `argc`                                          | 2          | 0xbfffffe5 | 0xbfffffe8 | 4            | process |
| fake return address (`esp` must point here)     | 0          | 0xbfffffe1 | 0xbfffffe4 | 4            | process |
| ...rest of the stack                            |            |            |            |              |         |
`esp`: 0xbfffffe1