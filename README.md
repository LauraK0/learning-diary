# learning-diary

### 20.10.22
Write a publishDateForDisplay function. Its job is to return the publish date for a blog post, formatted as a string, wrapped in a promise. We've provided a formatDate function, so you won't need to call any methods on the date objects.

publishDateForDisplay takes a date wrapped in a promise, like Promise.resolve(publishDate). If the date is undefined, it should return the string 'unpublished'. Otherwise it should return the result of formatDate(publishDate).

- function formatDate(date) {
  // Turn the date object into a string like '2024-11-19'
  return [date.getFullYear(), date.getMonth() + 1, date.getDate()]
    .join('-');
}

function publishDateForDisplay(publishDatePromise) {
  return publishDatePromise.then(publishDate => {
    if (publishDate === undefined) {
      return 'unpublished';
    } else {
      return formatDate(publishDate);
    }
  });
}

// Format one actual date and one undefined date.
const date1 = new Date('November 19, 2024 00:00:00');
const date2 = undefined;
publishDateForDisplay(Promise.resolve(date1)).then(formatted1 =>
  publishDateForDisplay(Promise.resolve(date2)).then(formatted2 =>
    [formatted1, formatted2]
  )
);


{fulfilled: ['2024-11-19', 'unpublished']}
