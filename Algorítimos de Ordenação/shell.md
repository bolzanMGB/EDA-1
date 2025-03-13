# Shell Sort
```cpp
void shell_sort(int v[], int l, int r)
{
    int h = 1; // h - distância

    // calcular o máximo h
    while (h < (r - l + 1) / 3) // (r - l + 1) / 9
        h = 3 * h + 1;

    while (h >= 1) {
        for (int i = l + h; i <= r; i++)
        {
            for (int j = i; j >= l + h && v[j] < v[j - h]; j -= h)
            {
                exch(v[j], v[j - h]);
            }
        }
        h = h / 3;
    }
}
```