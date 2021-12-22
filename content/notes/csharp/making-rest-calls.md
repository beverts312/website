---
title: Making Rest Calls in C#  
type: docs
---

These have been tested with .Net 4.5

### Basic Auth Example
```csharp
request.Headers.Authorization = new AuthenticationHeaderValue( "Basic", Convert.ToBase64String( ASCIIEncoding.ASCII.GetBytes( 
    string.Format( "{0}:{1}", user, password ) ) ) );
```

### Generic Request Example  
```csharp
public async Task<T> MakeRequest<T>( Uri uri ) 
{ 
     var client = new HttpClient { Timeout = new TimeSpan( 0, 0, Settings.Default.timeout ) }; 
     try 
     { 
          HttpResponseMessage response = await client.GetAsync( uri ); 
          if ( response.IsSuccessStatusCode ) 
          { 
               var content = await response.Content.ReadAsStringAsync( ); 
               try 
               { 
                    return JsonConvert.DeserializeObject<T>( content ); 
               } 
               catch ( Exception e ) 
               { 
                    throw new Exception( String.Format( "Error deserializing {0}, additional message: {1}", content, e.Message ) ); 
               } 
          } 
          else 
          { 
               throw new Exception( String.Format( "Error getting response from {0}, Status code: {1}", uri, response.StatusCode ) ); 
          } 
     } 
     catch ( Exception e ) 
     { 
          log.Error(string.Format("Request timed out to: {0}", uri)); 
          throw e; 
     } 
}
```