# Sawppy Six-Wheel Mars Rover: Build Guide

## 1. Before you start

Tools: 3D printer (200 x 200 mm bed or larger), hacksaw or chop saw with a metal blade, file, 8 mm hand reamer, soldering iron with heat-set insert tip, hex keys (M3), small Phillips screwdriver, pliers for E-clips, and a balance charger for the battery.

Plan for about 150 hours of printing in PETG. Start with the wheels and wheel hubs, since they take longest.

## 2. Print list

| Qty | Part file | Notes |
|---:|---|---|
| 88 | Clip2n125.stl | small extrusion clips, print spares |
| 12 | Clip3n20.stl | large extrusion clips, print spares |
| 6 | Wheel Hub.stl | print spares |
| 10 | LX-16A - Coupler.stl | print spares |
| 10 | LX-16A - Bracket.stl | |
| 6 | Wheel.stl | |
| 4 | Steering Knuckle.stl | |
| 4 | Body Corner.stl | |
| 2 | DiffBrace.stl | |
| 2 | DiffLink.stl | |
| 1 | DiffLower.stl | |
| 1 | DiffUpper.stl | |
| 2 | Rod Support.stl | |
| 1 | Power Panel.stl | |
| 2 | Fixed Knuckle.stl | one normal, one mirrored |
| 2 | Front Corner.stl | one normal, one mirrored |
| 2 | Rear Corner.stl | one normal, one mirrored |
| 2 | Bogie-Wheels.stl | one normal, one mirrored |
| 2 | Bogie-Body.stl | one normal, one mirrored |
| 2 | Rocker.stl | one normal, one mirrored |
| 2 | Rocker Body Mount.stl | one normal, one mirrored |
| 2 | DiffEnd.stl | one normal, one mirrored |
| 2 | Battery Tray.stl | one normal, one mirrored |

Settings: PETG, 0.4 mm nozzle, 0.2–0.3 mm layers, 3–4 perimeters, 30–40% infill. Print bearing seats and 8 mm bores slightly tight, then ream them to fit.

## 3. Cut the frame and shafts

15 mm extrusion (Misumi HFS3 or equivalent 1515 with 3 mm slot):

| Qty | Length (mm) | Purpose |
|---:|---:|---|
| 4 | 385 | body box, lengthwise |
| 4 | 245 | body box, widthwise |
| 1 | 238 | differential fixed beam |
| 2 | 182 | rocker joint to front wheel |
| 2 | 161 | rocker joint to bogie joint |
| 2 | 122 | bogie joint to middle wheel |
| 2 | 117 | bogie joint to rear wheel |

8 mm rod (the differential shaft must be steel; the rest can be steel or aluminum):

| Qty | Length (mm) | Part |
|---:|---:|---|
| 1 | 300 | differential shaft |
| 6 | 50 | wheel axles |
| 4 | 61 | steering shafts |
| 2 | 66.5 | bogie pivots |
| 2 | 84 | rocker pivots |

Cut grooves for the E-clips where the parts meet the bearings. The distance between grooves matters more than overall length. The 300 mm differential shaft has no grooves; set screws hold it at each end. Deburr every cut.

## 4. Actuator modules (x10)

1. New servos all ship with ID 1. Connect each servo alone to the USB adapter, give it its own ID, and write the ID on the case. Note which ID goes to which wheel; you enter that map in the rover software later.
2. Set the four steering servos to their center position before you fit the coupler, so the wheels point straight ahead.
3. Press a heat-set insert into each coupler, fit it to the servo horn with the small screws and fasten the servo into its bracket.

## 5. Wheels and corners

1. Press 608 bearings into the knuckles and corners. Ream any bore that is too tight; do not hammer bearings in.
2. Fit wheel hubs to the axles with M3 set screws on the flats, then mount the wheels.
3. Assemble the four steering corners (front and rear) and the two fixed middle knuckles.

## 6. Suspension

1. Build each bogie: bogie body, bogie wheel mount, the 122 mm and 117 mm extrusions, and the bogie pivot shaft with bearings and E-clips.
2. Build each rocker: rocker, the 182 mm and 161 mm extrusions, and the rocker pivot.
3. Check that each bogie swings freely before you go on.

## 7. Body and differential

1. Build the body box from the 385 mm and 245 mm extrusions with the four printed body corners and the clips.
2. Fit the 238 mm differential beam with the rod supports and the 300 mm steel shaft.
3. Connect the differential to each rocker with a turnbuckle, fastened with M3 x 16 mm bolts and no washers. The differential ends sit about 20 mm from the rocker body mounts. Adjust the turnbuckles until the body sits level with all six wheels on a flat floor.
4. Mount the rocker body mounts, then hang both rocker-bogie sides from the body.

## 8. Power and wiring

1. Battery tray, power panel, switch, fuse holder (10 A) and voltmeter go on the body. Wire battery → fuse → switch → servo bus power.
2. A 5 V buck converter set to 5.1 V feeds the Raspberry Pi from the same battery.
3. Daisy-chain all ten servos along the suspension arms, back to the USB adapter. Leave slack at every pivot and steering joint and tie the cables down so they cannot snag a wheel.

## 9. Software and first drive

- Raspberry Pi: install the SGVHAK rover software, set the serial port of the servo adapter and the servo IDs, then drive from a phone browser over Wi-Fi.
- Without a Pi: the ESP32 and Arduino sketches in the original project drive the same servo bus.
- First drive on blocks with the wheels off the ground. Check that every wheel spins the right way and that the corners steer the correct direction, then drive on the floor at low speed.

## Safety and limits

- Use a LiPo bag and a balance charger. Disconnect the battery for any wiring work.
- The servos are strong enough to pinch fingers in the steering joints.
- Sawppy is a model, not a weatherproof rover. Keep it out of water and wet grass.

## Troubleshooting

- Wheel jerks or stalls: the servo is in position mode instead of motor mode, or two servos share an ID.
- Rover pulls to one side: re-center the steering servos and check the turnbuckle lengths.
- Bearings loose: reprint with a slightly smaller bore or add a drop of retaining compound.

## Software and source links

- Rover software for the Raspberry Pi (phone-browser driving): https://github.com/Roger-random/SGVHAK_Rover
- ESP32 and Arduino sketches: `source/upstream/esp32_sawppy/` and `source/upstream/arduino_sawppy/` in this repository.
- Original Sawppy documentation (part notes, assembly photos, cut lists): `source/upstream/docs/` in this repository.
- Editable CAD (Onshape): https://cad.onshape.com/documents/43678ef564a43281c83e1aef
