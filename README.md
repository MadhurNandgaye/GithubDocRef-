Sure, I can help you convert this code to be used in a Material-UI `Table` component. Here's a modified version:

```jsx
<TableRow hover>
  <TableCell>
    <Stack direction="row">
      <Typography sx={{ paddingRight: 90 }} className="users-medium">
        {user.email}
      </Typography>
      <Typography className="users-medium">{user.firstName}</Typography>
      <Typography className="users-medium">{user.lastName}</Typography>
      <Typography className="users-medium">Admin</Typography>
    </Stack>
  </TableCell>
  <TableCell>
    <Stack direction="row" justifyContent="space-between">
      <ActionButton
        anchorEl={anchorEl}
        menuItems={UserContent.ROW_OPTIONS}
        open={open}
        handleActionClick={handleActionClick}
        handleClick={handleClick}
        handleClickAway={handleClickAway}
      />
    </Stack>
  </TableCell>
</TableRow>
```

This assumes you have imported `TableRow`, `TableCell`, `Stack`, `Typography`, `Divider`, and `ActionButton` from Material-UI. Make sure to adjust imports accordingly.