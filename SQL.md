# Show SQL

````
$current_costs = DB::select(
                  "SELECT w.alias, x.cost 
FROM ( SELECT ROW_NUMBER() OVER (PARTITION BY work_order_type_id  ORDER BY effective_date ) AS r, t.* 
       FROM work_order_costs t where effective_date > '$effective_date' ) x
       left join work_order_types w on w.id = x.work_order_type_id
WHERE x.r <= 1 order by work_order_type_id, effective_date;"
              );
````

See Laravel Debug Bar https://laravel-news.com/laravel-debugbar

Or in the code.

````
        \DB::connection()->enableQueryLog();
        $rows = DB::table('clients')
                    ->leftJoin('organizations',     'clients.organization_id',     '=', 'organizations.id')
                    ->select('clients.id as Id',
                        DB::raw('organizations.name || \' x  \' ||clients.name as Name'),

                             'clients.created_at as Created')
                    ->orderBy($column, $direction)
                    ->paginate(10);


        $query = \DB::getQueryLog();
        $lastQuery = end($query);

        dd($lastQuery);
````

# Raw Queries and Updates

Also see [Database](https://laravel.com/docs/5.3/database) which talks about  [fluent query builder](https://laravel.com/docs/5.3/queries), and the [Eloquent ORM](https://laravel.com/docs/5.3/eloquent).

# Left Join example 

in SourceFilesRepository.  One issue is all three tables had a `name` field so I had to use `AS` in the select.

See [https://laravel.com/docs/5.3/database#running-queries](https://laravel.com/docs/5.3/database#running-queries) for more information.

````
use Illuminate\Support\Facades\DB;
   .
   .
   .

    public function get_for_index(Request $request) {
         $sourceFiles = DB::table('source_files')
            ->leftJoin('organizations',     'source_files.organization_id',     '=', 'organizations.id')
            ->leftJoin('source_file_types', 'source_files.source_file_type_id', '=', 'source_file_types.id')
            ->select('source_files.id','source_files.name',
                            'organizations.name AS organization_name', 
                            'source_file_types.name AS source_file_type_name')
            ->get();

        return $sourceFiles;

    }
````

or _very raw input_

````
        $sql = "SELECT  source_files.id,
                        source_files.name,
                        organizations.name AS organization_name, 
                        source_file_types.name AS source_file_type_name 
                FROM source_files 
                LEFT JOIN organizations ON source_files.organization_id = organizations.id 
                LEFT JOIN source_file_types ON source_files.source_file_type_id = source_file_types.id";

        $sourceFiles = DB::select($sql);

        return $sourceFiles;
````

View looks like

````
    @foreach($sourceFiles as $sourceFiles)
        <tr>
            <td>{!! $sourceFiles->name !!}</td>
            <td>{!! $sourceFiles->organization_name !!}</td>
            <td>{!! $sourceFiles->source_file_type_name !!}</td>
            <td>
````

# To create or alter a column with raw sql
````
    public function up()
    {
        Schema::table('properties', function(Blueprint $table) {

            // See http://stackoverflow.com/questions/28787293/run-this-raw-sql-in-migration
            DB::connection()->getPdo()->exec('alter table properties add column geom geometry(MultiPolygon, 4326);');
        });
    }
````
