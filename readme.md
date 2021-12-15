Instructions

This projects is already set up preconfigured with TypeScript and Jasmine.

In the index.ts file in the src folder, you will see one complete function, and space to create 2 other functions.

In the indexSpec.ts files in src, you will see 2 specs and a space to create 1 more.

Your job is to look at the specs available, and write functions that pass on the index.ts file. Then, create the missing spec for the getRegionCountries function.

This assignment uses axios to get data from the restcountries.eu api. If you are unfamiliar with axios, follow the structure of the function getRegionCountries. Make sure to visit one of the routes to see how the JSON data is supplied from the API.

Make sure to run the test script when complete to ensure that the project builds and that all tests pass. View the package.json file to see available scripts.

NOTE: a popup of "Renderer Failure: tsconfig.json" may open when starting this project. It is safe to ignore this error. Error is due to the comments in tsconfig.json not being considered valid JSON; however, it is generally considered safe to place comments in JSON config files.




To Complete This Exercise:

    Run npm run test to ensure tests fail.
    View the tests on indexSpec.ts and the function on index.ts.
    Write the missing getCountry function, modeled from the getRegionCountries if you are unfamiliar with Axios.

async function getCountry(name: string) {
    const getApi = await axios(`https://restcountries.eu/rest/v2/name/${name}`);
    const data = getApi.data[0];
    return {
        capital: data.capital, 
        region: data.region,
        numericCode: data.numericCode
    };
}

    Write the missing getRegionCapitals function.
        Call the getRegionCountries to simplify the work.
        Create a countries array by running the second function.
        Create an array of api calls with the countries array and use Promise.all to create an array of responses
        Iterate through the array of responses to get each capital

async function getRegionCapitals(regionalbloc: string) {
    const countryEndpoints = await getRegionCountries(regionalbloc);
    const promises = countryEndpoints.map((endpoint: any) => 
       axios(`https://restcountries.eu/rest/v2/name/${endpoint}`
    ));
    const arr = await Promise.all(promises);
    const capitals = [];
    for (let i=0; i < arr.length; i++) {
        capitals.push(arr[i].data[0].capital);
    }
    return capitals;
}

    Write the test for getRegionCountries following the same structure as the two existing tests.

it("should get the countries in the region NAFTA", async () => {
    const data = await countries.getRegionCountries('nafta');
    expect(data).toEqual([
        'Canada', 'Mexico', 'United States of America'
    ]);
});

    Run npm run test to ensure your tests pass.

Thinking Like a Test Driven Developer

What hints did seeing the tests first give you in writing the functions? Did it help or did you prefer seeing the function and then writing the test?
Your reflection
It helps
Things to think about

When getting used to Test Driven Development, it can feel awkward at first getting used to writing tests first, but in time the benefits of recognizing edge cases and thinking out the problem before writing the functionality become more natural.
