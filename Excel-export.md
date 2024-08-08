# Controler
## Data should be a query
```
        return Excel::download(
            new ContractorTransferExport($query),
            $file_name);
```
## Filename
Give it a meaningful name with date time.
Replace Spaces and '/' character with '-'

```
   $file_name = $contractor->alias . "-Transfers" . Carbon::now()->format('Y-m-d H:i:s') . ".xlsx";
        $file_name = preg_replace('/[\\s_]/', '-', $file_name);
        $file_name = str_replace('/', '-', $file_name);
```


# For same column widths
```
use Maatwebsite\Excel\Concerns\Exportable;
use Maatwebsite\Excel\Concerns\FromQuery;
use Maatwebsite\Excel\Concerns\WithHeadings;
use Maatwebsite\Excel\Concerns\WithMapping;
use Maatwebsite\Excel\Concerns\ShouldAutoSize;
use Illuminate\Support\Carbon;

class ContractorTransferExport implements FromQuery, WithHeadings, WithMapping, ShouldAutoSize
{
    use Exportable;


```
