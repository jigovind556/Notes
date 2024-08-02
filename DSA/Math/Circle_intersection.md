# Code to find the intersection points of two circles


```cpp
#include <iostream>
#include <cmath>
#include <utility>

using namespace std;

pair<pair<double, double>, pair<double, double> > findCircleIntersections(double x1, double y1, double r1, double x2, double y2, double r2) {
    // Distance between circle centers
    double d = sqrt(pow(x2 - x1, 2) + pow(y2 - y1, 2));

    // Check if circles are too far apart or one is contained within the other
    if (d > r1 + r2 || d < fabs(r1 - r2)) {
        // No intersection
        return make_pair(make_pair(NAN, NAN), make_pair(NAN, NAN));
    }

    // Find the distance from the first circle's center to the intersection line
    double a = (pow(r1, 2) - pow(r2, 2) + pow(d, 2)) / (2 * d);

    // Height of the intersection points from the line
    double h = sqrt(pow(r1, 2) - pow(a, 2));

    // Find the midpoint between the two intersection points
    double x0 = x1 + a * (x2 - x1) / d;
    double y0 = y1 + a * (y2 - y1) / d;

    // Calculate the intersection points
    double rx = -(y2 - y1) * (h / d);
    double ry = (x2 - x1) * (h / d);

    pair<double, double> intersection1 = make_pair(x0 + rx, y0 + ry);
    pair<double, double> intersection2 = make_pair(x0 - rx, y0 - ry);

    return make_pair(intersection1, intersection2);
}

int main() {
    double x1, y1, r1, x2, y2, r2;

    cout << "Enter x1, y1, r1: ";
    cin >> x1 >> y1 >> r1;

    cout << "Enter x2, y2, r2: ";
    cin >> x2 >> y2 >> r2;

    pair<pair<double, double>, pair<double, double> > intersections = findCircleIntersections(x1, y1, r1, x2, y2, r2);

    if (isnan(intersections.first.first)) {
        cout << "The circles do not intersect." << endl;
    } else {
        cout << "Intersection points: " << endl;
        cout << "Point 1: (" << intersections.first.first << ", " << intersections.first.second << ")" << endl;
        cout << "Point 2: (" << intersections.second.first << ", " << intersections.second.second << ")" << endl;
    }

    return 0;
}
```