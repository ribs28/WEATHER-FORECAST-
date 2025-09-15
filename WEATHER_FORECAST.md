# WEATHER-FORECAST-
Develop a Weather Data Storage System using Python. The system will organize and manage weather-related data such as temperature, using 2D arrays and Abstract Data Types (ADTs).
class WeatherRecord:
    def __init__(self, date, city, temperature):
        self.date = date
        self.city = city
        self.temperature = temperature


class WeatherRecordADT:
    def __init__(self, years, cities):
        self.years = years
        self.cities = cities
        self.data = [[None for _ in range(len(cities))] for _ in range(len(years))]

    def insert(self, date, city, temperature):
        y = int(date[-4:])
        if y in self.years and city in self.cities:
            i = self.years.index(y)
            j = self.cities.index(city)
            self.data[i][j] = temperature

    def delete(self, date, city):
        y = int(date[-4:])
        if y in self.years and city in self.cities:
            i = self.years.index(y)
            j = self.cities.index(city)
            self.data[i][j] = None

    def retrieve(self, city, year):
        result = []
        if year in self.years and city in self.cities:
            i = self.years.index(year)
            j = self.cities.index(city)
            result.append(self.data[i][j])
        return result

    def row_major_access(self):
        result = []
        for i in range(len(self.years)):
            for j in range(len(self.cities)):
                result.append(self.data[i][j])
        return result

    def column_major_access(self):
        result = []
        for j in range(len(self.cities)):
            for i in range(len(self.years)):
                result.append(self.data[i][j])
        return result

    def handle_sparse_data(self):
        sparse = []
        for i in range(len(self.years)):
            for j in range(len(self.cities)):
                if self.data[i][j] is not None:
                    sparse.append((self.years[i], self.cities[j], self.data[i][j]))
        return sparse

    def analyze_complexity(self):
        return {
            "insert": "O(1)",
            "delete": "O(1)",
            "retrieve": "O(1)",
            "row_major_access": "O(n*m)",
            "column_major_access": "O(n*m)",
            "sparse_handling": "O(n*m)"
        }


# Example usage
years = [2024, 2025]
cities = ["Delhi", "Mumbai", "Chennai"]
w = WeatherRecordADT(years, cities)

w.insert("12/09/2025", "Delhi", 34)
w.insert("15/09/2025", "Mumbai", 30)
w.delete("15/09/2025", "Mumbai")
print("Row Major:", w.row_major_access())
print("Column Major:", w.column_major_access())
print("Sparse Data:", w.handle_sparse_data())
print("Complexity:", w.analyze_complexity())
