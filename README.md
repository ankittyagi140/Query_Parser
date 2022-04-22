# Query_Parser
for any given url parse the query param and return data in an object

const url= "https://www.baseurl.com/query?name=john%20doe&age=25&isMale=true&hobbies=fishing,%20racing,%20camping"
<!-- sample output={
              name: 'john doe',
              age: 25,
              isMale: true,
              hobbies: ['fishing', 'racing', 'camping']
              } -->
    
function manipulateUrl(url) {
  if (!url) {
    return;
  }
  const newUrl = url.split("?");
  const dataObject = decodeURI(newUrl[1]).split("&");
  const modifiedData = dataObject.map((el) => el.split("="));
  const finalObject = Object.fromEntries(modifiedData);
  const finalObjectData = { ...finalObject };
  console.log(finalObject);
  for (let key in finalObjectData) {
    if (key === "age") {
      finalObjectData[key] = +finalObjectData[key];
    }
    if (key === "hobbies") {
      finalObjectData[key] = finalObjectData[key].split(",");
    }
  }
  return finalObjectData;
}
const result = manipulateUrl(url);
console.log(result);
