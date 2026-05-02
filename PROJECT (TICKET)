#include <iostream>
#include <unordered_map>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

class TrainFareCalculator {
private:
    unordered_map<string, vector<pair<string, int>>> graph;

public:
    void addRoute(string from, string to, int distance) {
        graph[from].push_back({to, distance});
        graph[to].push_back({from, distance});
    }

    int shortestDistance(string source, string destination) {
        priority_queue<
            pair<int, string>,
            vector<pair<int, string>>,
            greater<pair<int, string>>
        > pq;

        unordered_map<string, int> dist;

        for (auto station : graph) {
            dist[station.first] = INT_MAX;
        }

        dist[source] = 0;
        pq.push({0, source});

        while (!pq.empty()) {
            int currentCost = pq.top().first;
            string currentStation = pq.top().second;
            pq.pop();

            if (currentStation == destination) {
                return currentCost;
            }

            for (auto neighbor : graph[currentStation]) {
                string nextStation = neighbor.first;
                int routeDistance = neighbor.second;

                int newDistance = currentCost + routeDistance;

                if (newDistance < dist[nextStation]) {
                    dist[nextStation] = newDistance;
                    pq.push({newDistance, nextStation});
                }
            }
        }

        return -1;
    }
};

int main() {
    TrainFareCalculator train;

    // Sample routes
    train.addRoute("Delhi", "Kanpur", 440);
    train.addRoute("Kanpur", "Lucknow", 90);
    train.addRoute("Lucknow", "Prayagraj", 200);
    train.addRoute("Delhi", "Jaipur", 280);
    train.addRoute("Jaipur", "Lucknow", 500);

    string source, destination;

    cout << "Enter source station: ";
    cin >> source;

    cout << "Enter destination station: ";
    cin >> destination;

    int distance = train.shortestDistance(source, destination);

    if (distance == -1) {
        cout << "Route not found!" << endl;
        return 0;
    }

    int farePerKm = 2;
    int totalFare = distance * farePerKm;

    cout << "Shortest Distance: " << distance << " km" << endl;
    cout << "Train Fare: Rs. " << totalFare << endl;

    return 0;
}
