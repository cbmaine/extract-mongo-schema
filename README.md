# Extract Mongo Schema

Extract (and visualize) schema from Mongo database, including foreign keys. Output is simple json file or html with dagre/d3.js diagram (depending on command line options).

## Instalation

```sh
npm -g install extract-mongo-schema
```

## Usage

```sh

Usage:
	extract-mongo-schema -d connection_string -o schema.json -f json
		-d, --database		Database connection string. Example: "mongodb://localhost:3001/meteor".
		-o, --output		Output file
		-f, --format		Output file format. Can be "json" or "html-diagram". Default is "json".
		-c, --collection	Comma separated list of collections to analyze. Example: "collection1,collection2".
		-a, --array		Comma separated list of types of arrays to analyze. Example: "Uint8Array,ArrayBuffer,Array".
		-r, --raw		Shows the exact list of types with frequency instead of the most frequent type only.

```


## Example usage

**Extract schema into json**

```
extract-mongo-schema -d "mongodb://localhost:3001/meteor" -o schema.json
```


**Extract schema into html**

```
extract-mongo-schema -d "mongodb://localhost:3001/meteor" -o schema.html -f html-diagram
```


**Extract specific collections in raw format and analyze Array items**

```
extract-mongo-schema -d "mongodb://localhost:3001/meteor" -o schema.json -c "collection1,collection2,collection3" -a "Array" -r
```

Open html in your browser and you'll see rendered ER diagram.

## Example output .html (screenshot)

![Alt text](/preview.png?raw=true "Preview")


## Example output .json

**schema.json**

```json
{
	"customers": {
		"_id": {
			"primaryKey": true,
			"type": "string",
			"required": true
		},
		"name": {
			"type": "string",
			"required": true
		},
		"phone": {
			"type": "string",
			"required": true
		},
		"email": {
			"type": "string",
			"required": true
		},
		"note": {
			"type": "string",
			"required": true
		},
		"createdAt": {
			"type": "Date",
			"required": true
		},
		"createdBy": {
			"key": true,
			"type": "string",
			"required": true
		},
		"modifiedAt": {
			"type": "Date",
			"required": true
		},
		"modifiedBy": {
			"key": true,
			"type": "string",
			"required": true
		},
		"ownerId": {
			"key": true,
			"type": "string",
			"required": true
		}
	},
	"invoices": {
		"_id": {
			"primaryKey": true,
			"type": "string",
			"required": true
		},
		"invoiceNumber": {
			"type": "string",
			"required": true
		},
		"date": {
			"type": "Date",
			"required": true
		},
		"customerId": {
			"foreignKey": true,
			"references": "customers",
			"key": true,
			"type": "string",
			"required": true
		},
		"createdAt": {
			"type": "Date",
			"required": true
		},
		"createdBy": {
			"key": true,
			"type": "string",
			"required": true
		},
		"modifiedAt": {
			"type": "Date",
			"required": true
		},
		"modifiedBy": {
			"key": true,
			"type": "string",
			"required": true
		},
		"ownerId": {
			"key": true,
			"type": "string",
			"required": true
		},
		"totalAmount": {
			"type": "number",
			"required": true
		}
	},
	"users": {
		"_id": {
			"primaryKey": true,
			"type": "string",
			"required": true
		},
		"createdAt": {
			"type": "Date",
			"required": true
		},
		"services": {
			"type": "Object",
			"structure": {
				"password": {
					"type": "Object",
					"structure": {
						"bcrypt": {
							"type": "string",
							"required": true
						}
					},
					"required": true
				},
				"resume": {
					"type": "Object",
					"structure": {
						"loginTokens": {
							"type": "Array",
							"required": true
						}
					},
					"required": true
				}
			},
			"required": true
		},
		"emails": {
			"type": "Array",
			"required": true
		},
		"roles": {
			"type": "Array",
			"required": true
		},
		"profile": {
			"type": "Object",
			"structure": {
				"name": {
					"type": "string",
					"required": true
				},
				"email": {
					"type": "string",
					"required": true
				},
				"facebook": {
					"type": "string",
					"required": true
				},
				"google": {
					"type": "string",
					"required": true
				},
				"twitter": {
					"type": "string",
					"required": true
				},
				"website": {
					"type": "string",
					"required": true
				}
			},
			"required": true
		}
	},
	"meteor_accounts_loginServiceConfiguration": {},
	"invoice_items": {
		"_id": {
			"primaryKey": true,
			"type": "string",
			"required": true
		},
		"description": {
			"type": "string",
			"required": true
		},
		"quantity": {
			"type": "number",
			"required": true
		},
		"price": {
			"type": "number",
			"required": true
		},
		"invoiceId": {
			"key": true,
			"foreignKey": true,
			"references": "invoices",
			"type": "string",
			"required": true
		},
		"createdAt": {
			"type": "Date",
			"required": true
		},
		"createdBy": {
			"key": true,
			"foreignKey": true,
			"references": "users",
			"type": "string",
			"required": true
		},
		"modifiedAt": {
			"type": "Date",
			"required": true
		},
		"modifiedBy": {
			"key": true,
			"foreignKey": true,
			"references": "users",
			"type": "string",
			"required": true
		},
		"ownerId": {
			"key": true,
			"foreignKey": true,
			"references": "users",
			"type": "string",
			"required": true
		},
		"amount": {
			"type": "number",
			"required": true
		}
	}
}
```


That's all folks.
Enjoy! :)
