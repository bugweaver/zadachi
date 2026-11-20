1. Min Stack
```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)

        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self) -> None:
        if not self.stack:
            raise IndexError("Stack is empty")

        val = self.stack.pop()

        if val == self.min_stack[-1]:
            self.min_stack.pop()

    def top(self) -> int:
        if not self.stack:
            raise IndexError("Stack is empty")

        return self.stack[-1]

    def get_min(self) -> int:
        if not self.min_stack:
            raise IndexError("Stack is empty")

        return self.min_stack[-1]
```

2. Design Underground System
```python
class UndergroundSystem:
    def __init__(self):
        self.check_ins = {}
        self.trips = {}

    def check_in(self, passenger_id: int, station: str, time: int) -> None:
        if passenger_id in self.check_ins:
            raise ValueError("Passenger is already checked in")

        self.check_ins[passenger_id] = (station, time)

    def check_out(self, passenger_id: int, station: str, time: int) -> None:
        if passenger_id not in self.check_ins:
            raise ValueError("Passenger has not checked in")

        start_station, start_time = self.check_ins.pop(passenger_id)

        route = (start_station, station)
        travel_time = time - start_time

        if route not in self.trips:
            self.trips[route] = [0, 0]

        self.trips[route][0] += travel_time
        self.trips[route][1] += 1

    def get_average_time(self, start_station: str, end_station: str) -> float:
        route = (start_station, end_station)

        if route not in self.trips:
            raise ValueError("No trips for this route")

        total_time, count = self.trips[route]

        return total_time / count
```
