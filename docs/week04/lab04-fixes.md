# Lab 04 Fix Log

1. StoreHeader | overflowed on the right at 320 dp | the Row gave a Column unbounded width | Expanded + maxLines + ellipsis; rating moved into the Column 
2. CategoryBar | overflowed on the right at 320 dp | six chips are wider than the screen and the Row cannot scroll | horizontal SingleChildScrollView 
3. PromoStrip / PromoCard | overflowed on the right at 320 dp | width: 200 forced a size and the parent did not share its space | Expanded per card + removed width: 200 
4. MenuTile | overflowed on the right with a long name | the Row gave a Column unbounded width; Spacer does not limit text | Expanded + maxLines: 2 + ellipsis, removed Spacer 
5. CartBar | overflowed on the right at 320 dp | Text had no limit, button fixed at 160 dp, height: 72 clips wrapped text | Expanded on Text, button sizes itself, height → minHeight 
6. MenuScreen (body) | overflowed on the bottom in landscape and with keyboard open | the children of the Column needed more height than was left, and a Column does not scroll | CustomScrollView with the header in SliverToBoxAdapter 
7. MenuScreen (list and grid) | all 500 items built at once, test 7 fails | a list of unknown length must be built lazily | SliverList.builder / SliverGrid.builder, no shrinkWrap 
8. MenuScreen (breakpoint) | layout chosen from screen width with > 600 | the decision must come from the constraints the parent gives, not the device size | LayoutBuilder with maxWidth >= 600 
9. MenuCard | overflowed on the bottom in the tablet grid | the grid cell gave a fixed height and the child forced height: 110 | icon area wrapped in Expanded + maxLines on texts + MaxCrossAxisExtent delegate 
10. PromoCard | fixed height: 150 overflows when text grows | the parent fixed a height without knowing the child | removed height, IntrinsicHeight + stretch in PromoStrip 
11. All long Text widgets | 200-character name exceeds the space | Text had no overflow strategy | maxLines + ellipsis |
12. PromoStrip | RangeError on promos[0] with zero items | the layout assumed at least two promos exist | PromoStrip(items:) takes 0 to 2 items and hides when empty 
13. MenuScreen (empty data) | blank screen with zero items | no state was designed for empty data | EmptyState (icon, message, action) with Key('empty-state') in SliverFillRemaining 
14. CartBar | order button under the gesture bar (bonus test) | Scaffold does not pad bottomNavigationBar and nothing read MediaQuery.padding | SafeArea(top: false) inside the coloured Container 
15. MenuScreen (body) | content under the notch in landscape | Scaffold does not pad the body on the left and right | SafeArea(top: false, bottom: false) around the LayoutBuilder 