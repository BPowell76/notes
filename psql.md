# PostgreSQL Notes

## Custom Domains
The following sections include SQL commands to create custom data types (Domains) for use in tables.
Using a `CHECK` constraint with regex, data uniformity and integrity can be enforced while also creating a single point of maintenance if a change needs to be made.

### Media
#### ISBNs
**ISBN 10**

ISBN 10 was the original method of identifying books until 2007.
Interestingly, there are more permutations of an ISBN 10 due to the check digit possible values being 0 through 10 versus 0 through 9.

```sql
CREATE DOMAIN isbn_10 AS char(13)
CHECK(
	VALUE ~ '\d{1}-\d{1}-\d{6}-\d{2}'
	OR VALUE ~ '\d{1}-\d{2}-\d{6}-\d{1}'
	OR VALUE ~ '\d{1}-\d{2}-\d{5}-\d{2}'
	OR VALUE ~ '\d{1}-\d{3}-\d{5}-\d{1}'
	OR VALUE ~ '\d{1}-\d{3}-\d{4}-\d{2}'
	OR VALUE ~ '\d{1}-\d{4}-\d{4}-\d{1}'
	OR VALUE ~ '\d{1}-\d{4}-\d{3}-\d{2}'
	OR VALUE ~ '\d{1}-\d{5}-\d{3}-\d{1}'
	OR VALUE ~ '\d{1}-\d{5}-\d{2}-\d{2}'
	OR VALUE ~ '\d{1}-\d{6}-\d{2}-\d{1}'
	OR VALUE ~ '\d{1}-\d{6}-\d{1}-\d{2}'
	OR VALUE ~ '\d{1}-\d{7}-\d{1}-\d{1}'
	OR VALUE ~ '\d{2}-\d{1}-\d{6}-\d{1}'
	OR VALUE ~ '\d{2}-\d{1}-\d{5}-\d{2}'
	OR VALUE ~ '\d{2}-\d{2}-\d{5}-\d{1}'
	OR VALUE ~ '\d{2}-\d{2}-\d{4}-\d{2}'
	OR VALUE ~ '\d{2}-\d{3}-\d{4}-\d{1}'
	OR VALUE ~ '\d{2}-\d{3}-\d{3}-\d{2}'
	OR VALUE ~ '\d{2}-\d{4}-\d{3}-\d{1}'
	OR VALUE ~ '\d{2}-\d{4}-\d{2}-\d{2}'
	OR VALUE ~ '\d{2}-\d{5}-\d{2}-\d{1}'
	OR VALUE ~ '\d{2}-\d{5}-\d{1}-\d{2}'
	OR VALUE ~ '\d{2}-\d{6}-\d{1}-\d{1}'
	OR VALUE ~ '\d{3}-\d{1}-\d{5}-\d{1}'
	OR VALUE ~ '\d{3}-\d{1}-\d{4}-\d{2}'
	OR VALUE ~ '\d{3}-\d{2}-\d{4}-\d{1}'
	OR VALUE ~ '\d{3}-\d{2}-\d{3}-\d{2}'
	OR VALUE ~ '\d{3}-\d{3}-\d{3}-\d{1}'
	OR VALUE ~ '\d{3}-\d{3}-\d{2}-\d{2}'
	OR VALUE ~ '\d{3}-\d{4}-\d{2}-\d{1}'
	OR VALUE ~ '\d{3}-\d{4}-\d{1}-\d{2}'
	OR VALUE ~ '\d{3}-\d{5}-\d{1}-\d{1}'
	OR VALUE ~ '\d{4}-\d{1}-\d{4}-\d{1}'
	OR VALUE ~ '\d{4}-\d{1}-\d{3}-\d{2}'
	OR VALUE ~ '\d{4}-\d{2}-\d{3}-\d{1}'
	OR VALUE ~ '\d{4}-\d{2}-\d{2}-\d{2}'
	OR VALUE ~ '\d{4}-\d{3}-\d{2}-\d{1}'
	OR VALUE ~ '\d{4}-\d{3}-\d{1}-\d{2}'
	OR VALUE ~ '\d{4}-\d{4}-\d{1}-\d{1}'
	OR VALUE ~ '\d{5}-\d{1}-\d{3}-\d{1}'
	OR VALUE ~ '\d{5}-\d{1}-\d{2}-\d{2}'
	OR VALUE ~ '\d{5}-\d{2}-\d{2}-\d{1}'
	OR VALUE ~ '\d{5}-\d{2}-\d{1}-\d{2}'
	OR VALUE ~ '\d{5}-\d{3}-\d{1}-\d{1}'
);
```

**ISBN 13**

ISBN 13 is an updated version of ISBN 10 that is more compliant with EAN-13 and incorporates the same data found in an ISBN 10.

```sql
CREATE DOMAIN isbn_13 AS char(17)
CHECK(
	VALUE ~ '^\d{3}-\d{1}-\d{2}-\d{6}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{1}-\d{3}-\d{5}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{1}-\d{4}-\d{4}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{1}-\d{5}-\d{3}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{1}-\d{6}-\d{2}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{1}-\d{7}-\d{1}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{2}-\d{1}-\d{6}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{2}-\d{2}-\d{5}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{2}-\d{3}-\d{4}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{2}-\d{4}-\d{3}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{2}-\d{5}-\d{2}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{2}-\d{6}-\d{1}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{3}-\d{1}-\d{5}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{3}-\d{2}-\d{4}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{3}-\d{3}-\d{3}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{3}-\d{4}-\d{2}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{3}-\d{5}-\d{1}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{4}-\d{1}-\d{4}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{4}-\d{2}-\d{3}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{4}-\d{3}-\d{2}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{4}-\d{4}-\d{1}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{5}-\d{1}-\d{3}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{5}-\d{2}-\d{2}-\d{1}'
	OR VALUE ~ '^\d{3}-\d{5}-\d{3}-\d{1}-\d{1}'
);
```
