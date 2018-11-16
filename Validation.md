# Rules to check if unique with two fields

Undocumented format

https://stackoverflow.com/questions/50349775/laravel-unique-validation-on-multiple-columns

````
table[,column[,ignore value[,ignore column[,where column,where value]...]]]
````

## Add
````
        $this->validate($request, [

            'name' => 'required|string|max:60|unique:city_neighborhoods,name,null,name,organization_id,' . intval(session('organization_id', null)) . ',name,' . $request->name,
             'short_name' => 'required|string|max:60|unique:city_neighborhoods,short_name,null,name,organization_id,' . intval(session('organization_id', null)) . ',name,' . $request->short_name,
           

        ], $this->messages);
````
##  Change
````
        $this->validate($request, [

            'name' => 'required|string|max:60|unique:owners,name,' . $request->name . ',name,organization_id,' . intval(session('organization_id', null)) . ',name,' . $request->name,

        ], $this->messages);
````
## Add using Rule
````
use Illuminate\Validation\Rule;
   .
   .
   .
        $organization_id = session('organization_id', 0);
        $this->validate($request, [
            'name' => [
                'required',
                'string',
                'max:60',
                Rule::unique('city_neighborhoods')->where(function ($query) use ($organization_id) {
                    return $query->where('organization_id', $organization_id);
                })
            ],
            ....
````

# After with JSON

````
use Illuminate\Validation\ValidationException;
use Illuminate\Http\Exceptions\HttpResponseException;
use Illuminate\Http\JsonResponse;

        $messages = [
            'description.required' => 'A Note is required',
        ];

        $validation_rules = [                 // FIXME need custome validation for request_id  must be 'N' or a number
            'type' => 'string|exists:work_order_types,alias',
        ];

        $validator = Validator::make($request->all(), $validation_rules, $messages);

        $validator->after(function ($validator) use ($request) {

            switch ($request->get('type')) {
                case 'trash':
                case 'brushlimbs':
                case 'tires':
                case 'bulky':
                    break;

                default:
                    $description = $request->get('description');
                    if (empty($description)) {
                        $validator->errors()->add('description', 'If you select bulky you must supply a description.');
                    }
            }
        });

        if ($validator->fails()) {
            $errors = (new ValidationException($validator))->errors();
            throw new HttpResponseException(response()->json(['errors' => $errors
            ], JsonResponse::HTTP_UNPROCESSABLE_ENTITY));
        }

````



# Custom Rules
## `OnlyDate`
This allows for a date of 4/1/2018, where the built-in rule did not allow for a single digit day or month.

````
use App\Rules\OnlyDate;
   .
   .
   .
        $this->validate($request, [
            'effective_date' => ['required', 'string', new OnlyDate],
````

## `exists_or_null`

Validate exists_or_null or 0,-1,null


Usage:

````
        $validation_rules = [
            'external_vendor_id' => 'integer|exists_or_null:client_vendors,id',
        ];

        $this->validate($request, $validation_rules , $this->messages);
````

## `exists_or_n`

Validate exists_or_n or N,-1


Usage:

````
        $validation_rules = [
            'responsible_id' => 'required|exists_or_n:users,id',
        ];

        $this->validate($request, $validation_rules , $this->messages);
````

# How to make a Custom Validation Rule.

## Laravel documentation

See [Custom Validation Rules](https://laravel.com/docs/5.6/validation#custom-validation-rules)

The starting point is

````
php artisan make:rule Uppercase
````

Usage:

````
use App\Rules\Uppercase;

$request->validate([
    'name' => ['required', 'string', new Uppercase],
]);
````

## Works but could be better

Located in: `Providers/AppServiceProvider.php . AppServiceProvider::boot()`

````
        /**
         * Validate ExistsInDatabase or 0/null
         * From: https://laracasts.com/discuss/channels/laravel/validator-ignoring-field-if-value-is-0-for-exists-rule
         *
         * Can be used like
         *
         *    'parent_id' => 'sometimes|exists_or_null:company_categories,id'
         */
        Validator::extend(
            'exists_or_null',
            function ($attribute, $value, $parameters)
            {
                if($value == 0 || $value == -1 || is_null($value)) {
                    return true;
                } else {
                    $validator = Validator::make([$attribute => $value], [
                        $attribute => 'exists:' . implode(",", $parameters)
                    ]);
                    return !$validator->fails();
                }
            }
        );
````

Usage:

````
        $validation_rules = [                 // FIXME need custome validation for request_id  must be 'N' or a number
            'external_vendor_id' => 'integer|exists_or_null:client_vendors,id',
        ];

        $this->validate($request, $validation_rules , $this->messages);
````
