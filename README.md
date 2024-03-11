Certainly, I've cleaned up the code for better readability while keeping the functionality intact:

```jsx
<TableHead>
  <TableRow className="tr-default">
    {columns.map((_column, index) => {
      const isColumnActive = _column.active;
      const isOrderByColumn = orderBy === _column.dataProperty;
      const displayStyle = { display: isColumnActive ? null : 'none' };

      return (
        <TableCell
          key={_column.dataProperty}
          sx={displayStyle}
          sortDirection={isOrderByColumn ? order : false}
          className="tablehead-cell"
        >
          <TableSortLabel
            disabled={editable}
            active={isOrderByColumn}
            direction={isOrderByColumn ? order : 'asc'}
            onClick={() => handleRequestSort(_column.dataProperty)}
          >
            <Typography sx={{ fontWeight: '500' }}>
              {VendorContent.VENDOR_PRODUCT_COLUMNS_FOR_RANKING[index]}
            </Typography>
          </TableSortLabel>
        </TableCell>
      );
    })}
  </TableRow>
</TableHead>
```

This version uses more descriptive variable names and breaks down the mapping logic into a cleaner structure. The functionality remains the same. If you have any specific preferences or additional requirements, feel free to let me know.
