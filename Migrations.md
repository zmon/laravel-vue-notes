
````
 public function up()
    {
        // You can do anything, ie add a record, change, delete
        
        $workOrderRole = \App\WorkOrderRole::create(['id' => 1108, 'organization_id' => 1, 'name' => 'CONTRACTOR', 'scope' => 'CONTRACTOR',   'sequence' => 8, 'alias' => 'CONTRACTOR']);

        // Do SQL
        
        DB::connection()->getPdo()->exec('DELETE FROM kcmo_gis;');

        // Create a table
        Schema::create('work_order_costs', function (Blueprint $table) {
            $table->increments('id');
            $table->integer('organization_id');

            $table->timestamps();

            $table->integer('created_by')->default(0)->after('created_at')->nullable();
            $table->integer('modified_by')->default(0)->after('updated_at')->nullable();
            $table->integer('purged_by')->default(0)->after('deleted_at')->nullable();

        });
        
        // Modify a table
        
        Schema::table('kcmo_gis', function(Blueprint $table)
        {
            // add columns
            $table->string('land_use_code',10)->nullable()->default('');
            $table->string('land_use_description',60)->nullable()->default('');
            
            // change columns
            $table->string('title', 60)->change();
            $table->string('name', 30)->change();
            
            //Create and drop indexs
            $table->unique(array('organization_id', 'title'));
            $table->dropUnique('contracts_name_unique');
            $table->dropUnique('contracts_title_unique');

        });
        
        
    }
    
public function down()
    {

        Schema::drop('work_order_costs');
        
        Schema::table('work_order_types', function ($table) {
            $table->dropColumn('mark_mowed_sequence');
        });

    }
    
````    

    
