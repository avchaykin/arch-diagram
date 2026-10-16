Create web application, to create architecture diagrams. 

Requirements :
1. Create block : size, color, border style/color, title (rich text with line breaks), icon, badge (to highlight block)
2. Create link : link is created from block by dragging with shift key and connected to other block (or not / free link)
3. Connectors on block created automatically on any side, after it can be dragged to other side or other block. They can be simple (no additional element), with circle or square. Color of connector can be set up
4. Links can have no ends or arrows (full, lined narrow/wide), circles, triangles, squares
5. Links can be traced as curves, lines or polylines
6. Polylines should avoid overlapping (with a tolerance distance), going under the block (or very near to it)
7. Polylines should have radius in connections
8. Setting should be provided (for defaults and visual settings)

Other things:
- Init git, all changes should be commited
- Create public repo in github and push it (initally and after on request)
- Single html/jss without server
- Store all data in json
- Can work with local files read/write (with Google Chrome)
- Json should store info about application : version + link to github
