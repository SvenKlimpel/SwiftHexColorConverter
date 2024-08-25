#  🔥Easy extension of Color to use convert HexColors to UIColors in Swift
## This simple extension makes it possible to use hexCodes while programmingin Swift. I did not create it myself (just asked chatGPT lol) , but wanted to share it on my profile to make it more easily accesible

### 🎨 Where to find some cool Colourpalettes:
- Just Ask ChatGPT for some Colours, that represent the athmosphere you want to create
- [Another helpful website](https://www.color-hex.com)



# 🧑‍💻 The Code 
```

import Foundation
import SwiftUI
// Examples of Colors you can add with this
public let Softsand: Color = Color(hex:"#eee0ca")
public let blushBeige: Color = Color(hex:"#e1ccb7")
public let warmAlmond: Color = Color(hex:"#ddbea5")
public let creamyOat: Color = Color(hex:"#e5dfc3")
public let dustyRose: Color = Color(hex:"#ddc6c6")


extension Color {
    init(hex: String) {
        let hex = hex.trimmingCharacters(in: CharacterSet.alphanumerics.inverted)
        var int: UInt64 = 0
        Scanner(string: hex).scanHexInt64(&int)
        
        let r, g, b, a: UInt64
        switch hex.count {
        case 3: // RGB (12-bit)
            (r, g, b, a) = ((int >> 8) * 17, (int >> 4 & 0xF) * 17, (int & 0xF) * 17, 255)
        case 6: // RGB (24-bit)
            (r, g, b, a) = (int >> 16, int >> 8 & 0xFF, int & 0xFF, 255)
        case 8: // ARGB (32-bit)
            (r, g, b, a) = (int >> 16 & 0xFF, int >> 8 & 0xFF, int & 0xFF, int >> 24)
        default:
            (r, g, b, a) = (1, 1, 1, 1) // Default to white if invalid hex string
        }
        
        self.init(
            .sRGB,
            red: Double(r) / 255,
            green: Double(g) / 255,
            blue: Double(b) / 255,
            opacity: Double(a) / 255
        )
    }
}
```
