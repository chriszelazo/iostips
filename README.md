# iOS Tips n Tricks
Nuggests of iOS knowledge.

## Contents
- Autolayout

## AutoLayout
Online autolayout error debugger: [WTF Autolayout](https://www.wtfautolayout.com/).

## UIFont
Using system fonts: (*SF Pro* as of iOS 11.0)
```
UIFont.systemFont(ofSize: 18.0, weight: .bold)
UIFont.monospacedDigitSystemFont(ofSize: 18.0, weight: .regular)
```

Custom fonts:
[List of fonts](http://iosfonts.com/) shipped with iOS.
```
UIFont(name: "SFProDisplay-Bold", size: 18.0)
```

## UIImageView
Load a remote image into an instance of `UIImageView`.
Usage: `myImageView.load("www.mycdn.com/image.png")`
```
public extension UIImageView {

    public func loadImage(_ urlString: String) {
        // Reset image in case one is already showing
        self.image = nil
        
        // Build new URL
        guard let url = URL(string: urlString) else {
            print("Invalid URL: \(urlString)")
            return
        }
        
        // Download and set image
        URLSession.shared.dataTask(with: url, completionHandler: { (data, response, error) -> Void in
            guard error == nil, let data = data, let image = UIImage(data: data) else {
                print("Failed to load image: \(error)")
                return
            }
            // Update the image on main thread
            DispatchQueue.main.async {
                self.image = image
            }
        }).resume() // Tells the data task to begin.
    }
    
}
```

## UIView
Rounded corners on any UIView subclass.
```
view.layer.cornerRadius = 8.0
view.clipsToBounds = true
```

