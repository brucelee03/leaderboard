# Making API Call with Hooks

# Making API Call with Hooks

## API Call Logic

```js
const url = 'https://apis.ccbp.in/leaderboard'
const options = {
  method: 'GET',
  headers: {
    Authorization:
      'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InJhaHVsIiwicm9sZSI6IlBSSU1FX1VTRVIiLCJpYXQiOjE2MjMwNjU1MzJ9.D13s5wN3Oh59aa_qtXMo3Ec4wojOx0EZh8Xr5C5sRkU',
  },
}
const response = await fetch(url, options)
const responseData = await response.json()
```

## Maintaining API Response in the State

```js
const apiStatusConstants = {
  initial: 'INITIAL',
  inProgress: 'IN_PROGRESS',
  success: 'SUCCESS',
  failure: 'FAILURE',
}
```

## Add the below methods in Leaderboard Component to render views

```js
const renderLoadingView = () => {}
const renderSuccessView = () => {}
const renderFailureView = () => {}
```

## Add the below statements in renderLeaderboard method to render Views Based on the API Status

```js
const renderLeaderboard = () => {
  const {status} = apiResponse
  switch (status) {
    case apiStatusConstants.inProgress:
      return renderLoadingView()
    case apiStatusConstants.success:
      return renderSuccessView()
    case apiStatusConstants.failure:
      return renderFailureView()
    default:
      return null
  }
}
```

## Add the below statements in your code to import React Loader Spinner

```js
import Loader from 'react-loader-spinner'
```

## Add this code to render loading view

```js
<LoadingViewContainer>
  <Loader type="ThreeDots" color="#ffffff" height="50" width="50" />
</LoadingViewContainer>
```

## Add this code to Format the data that we got in the API Response

```js
const {data} = apiResponse
const formattedLeaderboardData = data.leaderboard_data.map(eachUser => ({
  id: eachUser.id,
  rank: eachUser.rank,
  name: eachUser.name,
  profileImgUrl: eachUser.profile_image_url,
  score: eachUser.score,
  language: eachUser.language,
  timeSpent: eachUser.time_spent,
}))
```

## Add this code to render LeaderboardTable

```js
return <LeaderboardTable leaderboardData={formattedLeaderboardData} />
```

## Add this code to render failure view

```js
const {errorMsg} = apiResponse
return <ErrorMessage>{errorMsg}</ErrorMessage>
```
