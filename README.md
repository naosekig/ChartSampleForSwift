# ChartSampleForSwift
Pie chart with round start and end points - Swift

```
import UIKit

class ChartView:UIView {
    let caShapeLayerForBase:CAShapeLayer = CAShapeLayer.init()
    let caShapeLayerForValue:CAShapeLayer = CAShapeLayer.init()

    func drawChart(rate:Double){
        drawBaseChart()
        drawValueChart(rate: rate)

        let caBasicAnimation = CABasicAnimation(keyPath: "strokeEnd")
        caBasicAnimation.duration = 2.0
        caBasicAnimation.fromValue = 0.0
        caBasicAnimation.toValue = 1.0
        caShapeLayerForValue.add(caBasicAnimation, forKey: "chartAnimation")
    }

    private func drawBaseChart(){
        let shapeFrame = CGRect.init(x: 0, y: 0, width: self.frame.width, height: self.frame.height)
        caShapeLayerForBase.frame = shapeFrame
        caShapeLayerForBase.strokeColor = UIColor(displayP3Red: 1, green: 0.8, blue: 0.4, alpha: 1.0).cgColor
        caShapeLayerForBase.fillColor = UIColor.clear.cgColor
        caShapeLayerForBase.lineWidth = 50
        caShapeLayerForBase.lineCap = .round

        let startAngle:CGFloat = CGFloat(0.0)
        let endAngle:CGFloat = CGFloat(Double.pi * 2.0)

        caShapeLayerForBase.path = UIBezierPath.init(arcCenter: CGPoint.init(x: shapeFrame.size.width / 2.0, y: shapeFrame.size.height / 2.0),radius: shapeFrame.size.width / 2.0,startAngle: startAngle,endAngle: endAngle,clockwise: true).cgPath
        self.layer.addSublayer(caShapeLayerForBase)
    }

    private func drawValueChart(rate:Double){
        let shapeFrame = CGRect.init(x: 0, y: 0, width: self.frame.width, height: self.frame.height)
        caShapeLayerForValue.frame = shapeFrame

        caShapeLayerForValue.strokeColor = UIColor(displayP3Red: 1, green: 0.4, blue: 0.4, alpha: 1).cgColor
        caShapeLayerForValue.fillColor = UIColor.clear.cgColor
        caShapeLayerForValue.lineWidth = 50
        caShapeLayerForValue.lineCap = .round

        let startAngle:CGFloat = CGFloat(-1 * Double.pi / 2.0)

        let endAngle :CGFloat = CGFloat(rate / 100 * Double.pi * 2.0 - (Double.pi / 2.0))

        caShapeLayerForValue.path = UIBezierPath.init(arcCenter: CGPoint.init(x: shapeFrame.size.width / 2.0, y: shapeFrame.size.height / 2.0),radius: shapeFrame.size.width / 2.0,startAngle: startAngle,endAngle: endAngle,clockwise: true).cgPath
        self.layer.addSublayer(caShapeLayerForValue)
    }
}
```
