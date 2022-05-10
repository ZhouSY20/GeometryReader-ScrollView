# GeometryReader-ScrollView
## Topics
GeometryReader, ScrollView
## Screenshots
![image](https://user-images.githubusercontent.com/103715094/167536538-3783cd11-0034-4229-a91e-1fe0afc26822.png)

## The view without GeometryReader
![scrollView1](https://user-images.githubusercontent.com/103715094/167535356-0d74eea9-40e7-4942-a9c3-e87ce45af2ba.jpg)

### The view without GeometryReader
```swift
        var body: some View {
            ScrollView(.horizontal, showsIndicators: false, content:  {
                HStack{
                    ForEach(0..<8) { index in
                        RoundedRectangle(cornerRadius: 20)
                            .frame(width: 300, height: 450)
                            .padding()
                    }
                }
            })

```
### Use Geometry to change the degrees to change the angle
```swift
    func getPercentage(geo: GeometryProxy) -> Double {
        let maxDistance = UIScreen.main.bounds.width / 2
        let currentX = geo.frame(in: .global).midX
        return Double( 1 - (currentX / maxDistance))
    }

    var body: some View {
        ScrollView(.horizontal, showsIndicators: false, content:  {
            HStack{
                ForEach(0..<8) { index in
                    GeometryReader { geometry in
                        RoundedRectangle(cornerRadius: 20)
                            .rotation3DEffect(
                                Angle(degrees: getPercentage(geo: geometry) * 20),
                                axis: (x: 0.0, y: 1.0, z: 0.0))

                    }
                    .frame(width: 300, height: 450)
                    .padding()


                }
            }
        })
```

