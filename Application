
import java.awt.*;
import java.awt.event.*;
import java.util.*;
import javax.swing.*;
import javax.swing.border.*;

// ─────────────────────────────────────────────
//  ABSTRACT BASE RESTAURANT
// ─────────────────────────────────────────────
abstract class Restaurant {

    protected double totalAmount = 0;
    protected Map<String, Integer> itemQuantities = new LinkedHashMap<>();

    protected abstract String getName();

    protected abstract Color getThemeColor();

    protected abstract Color getAccentColor();

    protected abstract String getEmoji();

    protected abstract Map<String, Double> getMenuItems();

    protected abstract Map<String, String> getItemEmojis();

    public void addItem(String item) {
        itemQuantities.merge(item, 1, Integer::sum);
        totalAmount += getMenuItems().get(item);
    }

    public void removeItem(String item) {
        if (itemQuantities.containsKey(item) && itemQuantities.get(item) > 0) {
            itemQuantities.merge(item, -1, Integer::sum);
            totalAmount -= getMenuItems().get(item);
            if (itemQuantities.get(item) <= 0) {
                itemQuantities.remove(item);
            }
        }
    }

    public double getTotalAmount() {
        return totalAmount;
    }

    public Map<String, Integer> getItemQuantities() {
        return itemQuantities;
    }
}

// ─────────────────────────────────────────────
//  RESTAURANT IMPLEMENTATIONS
// ─────────────────────────────────────────────
class McDonalds extends Restaurant {

    @Override
    public String getName() {
        return "McDonald's";
    }

    @Override
    public Color getThemeColor() {
        return new Color(18, 18, 18);
    }

    @Override
    public Color getAccentColor() {
        return new Color(255, 188, 0);
    }

    @Override
    public String getEmoji() {
        return "🍟";
    }

    @Override
    public Map<String, Double> getMenuItems() {
        Map<String, Double> m = new LinkedHashMap<>();
        m.put("Donut", 500.0);
        m.put("Ice Cream", 400.0);
        m.put("Coffee", 300.0);
        return m;
    }

    @Override
    public Map<String, String> getItemEmojis() {
        Map<String, String> e = new LinkedHashMap<>();
        e.put("Donut", "🍩");
        e.put("Ice Cream", "🍦");
        e.put("Coffee", "☕");
        return e;
    }
}

class Howdy extends Restaurant {

    @Override
    public String getName() {
        return "Howdy";
    }

    @Override
    public Color getThemeColor() {
        return new Color(15, 15, 15);
    }

    @Override
    public Color getAccentColor() {
        return new Color(255, 100, 30);
    }

    @Override
    public String getEmoji() {
        return "🍔";
    }

    @Override
    public Map<String, Double> getMenuItems() {
        Map<String, Double> m = new LinkedHashMap<>();
        m.put("Burger", 800.0);
        m.put("Fries", 250.0);
        m.put("Pizza", 150.0);
        return m;
    }

    @Override
    public Map<String, String> getItemEmojis() {
        Map<String, String> e = new LinkedHashMap<>();
        e.put("Burger", "🍔");
        e.put("Fries", "🍟");
        e.put("Pizza", "🍕");
        return e;
    }
}

class Ranchers extends Restaurant {

    @Override
    public String getName() {
        return "Ranchers";
    }

    @Override
    public Color getThemeColor() {
        return new Color(12, 18, 12);
    }

    @Override
    public Color getAccentColor() {
        return new Color(80, 200, 80);
    }

    @Override
    public String getEmoji() {
        return "🍗";
    }

    @Override
    public Map<String, Double> getMenuItems() {
        Map<String, Double> m = new LinkedHashMap<>();
        m.put("Zinger", 400.0);
        m.put("Nuggets", 500.0);
        m.put("Juice", 200.0);
        return m;
    }

    @Override
    public Map<String, String> getItemEmojis() {
        Map<String, String> e = new LinkedHashMap<>();
        e.put("Zinger", "🌶️");
        e.put("Nuggets", "🍗");
        e.put("Juice", "🧃");
        return e;
    }
}

// ─────────────────────────────────────────────
//  UI HELPERS
// ─────────────────────────────────────────────
class UIHelper {

    static final Color BG = new Color(13, 13, 13);
    static final Color SURFACE = new Color(22, 22, 22);
    static final Color CARD = new Color(30, 30, 30);
    static final Color TEXT = new Color(245, 245, 245);
    static final Color MUTED = new Color(140, 140, 140);
    static final Color BORDER = new Color(45, 45, 45);

    static Font font(int style, int size) {
        return new Font("Segoe UI", style, size);
    }

    static JLabel label(String text, Font font, Color color) {
        JLabel l = new JLabel(text);
        l.setFont(font);
        l.setForeground(color);
        return l;
    }

    /**
     * Rounded panel with fill color
     */
    static JPanel roundPanel(Color bg, int radius) {
        return new JPanel() {
            @Override
            protected void paintComponent(Graphics g) {
                Graphics2D g2 = (Graphics2D) g.create();
                g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
                g2.setColor(bg);
                g2.fillRoundRect(0, 0, getWidth(), getHeight(), radius, radius);
                g2.dispose();
            }
        };
    }

    /**
     * Pill button
     */
    static JButton pillButton(String text, Color bg, Color fg, int radius) {
        JButton btn = new JButton(text) {
            @Override
            protected void paintComponent(Graphics g) {
                Graphics2D g2 = (Graphics2D) g.create();
                g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
                g2.setColor(getModel().isPressed() ? bg.darker()
                        : getModel().isRollover() ? bg.brighter() : bg);
                g2.fillRoundRect(0, 0, getWidth(), getHeight(), radius, radius);
                g2.setColor(fg);
                FontMetrics fm = g2.getFontMetrics();
                int x = (getWidth() - fm.stringWidth(getText())) / 2;
                int y = (getHeight() + fm.getAscent() - fm.getDescent()) / 2;
                g2.drawString(getText(), x, y);
                g2.dispose();
            }
        };
        btn.setFont(font(Font.BOLD, 13));
        btn.setForeground(fg);
        btn.setPreferredSize(new Dimension(110, 38));
        btn.setContentAreaFilled(false);
        btn.setBorderPainted(false);
        btn.setFocusPainted(false);
        btn.setCursor(Cursor.getPredefinedCursor(Cursor.HAND_CURSOR));
        return btn;
    }

    static void styleFrame(JFrame f) {
        f.getContentPane().setBackground(BG);
        f.getRootPane().setBorder(BorderFactory.createLineBorder(BORDER, 1));
    }
}

// ─────────────────────────────────────────────
//  ORDER SCREEN
// ─────────────────────────────────────────────
class OrderScreen extends JFrame {

    private final Restaurant restaurant;
    private final Map<String, JLabel> qtyLabels = new HashMap<>();
    private JLabel totalLabel;
    private JPanel cartPanel;

    public OrderScreen(Restaurant r) {
        this.restaurant = r;
        setTitle(r.getName() + " — Order");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(820, 600);
        setLocationRelativeTo(null);
        setResizable(false);
        UIHelper.styleFrame(this);
        buildUI();
        setVisible(true);
    }

    private void buildUI() {
        JPanel root = new JPanel(new BorderLayout(0, 0));
        root.setBackground(UIHelper.BG);

        // ── LEFT PANEL (menu) ──
        JPanel left = new JPanel();
        left.setBackground(UIHelper.BG);
        left.setLayout(new BoxLayout(left, BoxLayout.Y_AXIS));
        left.setBorder(BorderFactory.createEmptyBorder(30, 30, 30, 16));
        left.setPreferredSize(new Dimension(480, 0));

        // Header
        JLabel emoji = UIHelper.label(restaurant.getEmoji() + "  " + restaurant.getName(),
                UIHelper.font(Font.BOLD, 26), UIHelper.TEXT);
        JLabel sub = UIHelper.label("Select items to add to your order",
                UIHelper.font(Font.PLAIN, 13), UIHelper.MUTED);
        left.add(emoji);
        left.add(Box.createVerticalStrut(4));
        left.add(sub);
        left.add(Box.createVerticalStrut(24));

        // Menu items
        Map<String, Double> menu = restaurant.getMenuItems();
        Map<String, String> emojis = restaurant.getItemEmojis();
        for (String item : menu.keySet()) {
            left.add(buildMenuCard(item, menu.get(item), emojis.getOrDefault(item, "🍽️")));
            left.add(Box.createVerticalStrut(12));
        }

        // ── RIGHT PANEL (cart) ──
        JPanel right = new JPanel(new BorderLayout());
        right.setBackground(UIHelper.SURFACE);
        right.setBorder(BorderFactory.createEmptyBorder(30, 16, 24, 24));
        right.setPreferredSize(new Dimension(340, 0));

        JLabel cartTitle = UIHelper.label("🛒  Your Order", UIHelper.font(Font.BOLD, 18), UIHelper.TEXT);
        right.add(cartTitle, BorderLayout.NORTH);

        cartPanel = new JPanel();
        cartPanel.setLayout(new BoxLayout(cartPanel, BoxLayout.Y_AXIS));
        cartPanel.setBackground(UIHelper.SURFACE);
        JScrollPane sp = new JScrollPane(cartPanel);
        sp.setBorder(null);
        sp.setBackground(UIHelper.SURFACE);
        sp.getViewport().setBackground(UIHelper.SURFACE);
        right.add(sp, BorderLayout.CENTER);

        // Bottom total + place order
        JPanel bottom = new JPanel();
        bottom.setLayout(new BoxLayout(bottom, BoxLayout.Y_AXIS));
        bottom.setBackground(UIHelper.SURFACE);
        bottom.setBorder(new MatteBorder(1, 0, 0, 0, UIHelper.BORDER));

        JPanel totalRow = new JPanel(new BorderLayout());
        totalRow.setBackground(UIHelper.SURFACE);
        totalRow.setBorder(BorderFactory.createEmptyBorder(14, 0, 10, 0));
        totalLabel = UIHelper.label("Total: Rs. 0", UIHelper.font(Font.BOLD, 16), UIHelper.TEXT);
        totalRow.add(totalLabel, BorderLayout.WEST);
        bottom.add(totalRow);

        JButton placeBtn = UIHelper.pillButton("Place Order →",
                restaurant.getAccentColor(),
                restaurant.getName().equals("McDonald's") ? Color.BLACK : Color.WHITE, 10);
        placeBtn.setPreferredSize(new Dimension(280, 44));
        placeBtn.setMaximumSize(new Dimension(Integer.MAX_VALUE, 44));
        placeBtn.addActionListener(e -> {
            if (restaurant.getTotalAmount() == 0) {
                JOptionPane.showMessageDialog(this, "Please add at least one item!", "Empty Cart",
                        JOptionPane.WARNING_MESSAGE);
                return;
            }
            dispose();
            new ReceiptScreen(restaurant);
        });
        bottom.add(placeBtn);

        right.add(bottom, BorderLayout.SOUTH);

        root.add(left, BorderLayout.WEST);
        root.add(right, BorderLayout.CENTER);
        setContentPane(root);
    }

    private JPanel buildMenuCard(String item, double price, String emoji) {
        JPanel card = UIHelper.roundPanel(UIHelper.CARD, 14);
        card.setLayout(new BorderLayout(12, 0));
        card.setBorder(BorderFactory.createEmptyBorder(14, 16, 14, 14));
        card.setMaximumSize(new Dimension(Integer.MAX_VALUE, 72));

        // Emoji badge
        JLabel emojiLbl = new JLabel(emoji, SwingConstants.CENTER);
        emojiLbl.setFont(new Font("Segoe UI Emoji", Font.PLAIN, 28));
        emojiLbl.setPreferredSize(new Dimension(48, 48));
        JPanel emojiBadge = UIHelper.roundPanel(new Color(40, 40, 40), 10);
        emojiBadge.setPreferredSize(new Dimension(54, 54));
        emojiBadge.setLayout(new BorderLayout());
        emojiBadge.add(emojiLbl, BorderLayout.CENTER);

        // Name & price
        JPanel info = new JPanel();
        info.setOpaque(false);
        info.setLayout(new BoxLayout(info, BoxLayout.Y_AXIS));
        JLabel nameLbl = UIHelper.label(item, UIHelper.font(Font.BOLD, 14), UIHelper.TEXT);
        JLabel priceLbl = UIHelper.label("Rs. " + (int) price, UIHelper.font(Font.PLAIN, 12),
                restaurant.getAccentColor());
        info.add(nameLbl);
        info.add(Box.createVerticalStrut(3));
        info.add(priceLbl);

        // Qty controls
        JPanel ctrl = new JPanel(new FlowLayout(FlowLayout.RIGHT, 6, 0));
        ctrl.setOpaque(false);

        JLabel qty = UIHelper.label("0", UIHelper.font(Font.BOLD, 15), UIHelper.TEXT);
        qty.setPreferredSize(new Dimension(22, 20));
        qty.setHorizontalAlignment(SwingConstants.CENTER);
        qtyLabels.put(item, qty);

        JButton minus = roundIconButton("−", new Color(50, 50, 50));
        JButton plus = roundIconButton("+", restaurant.getAccentColor());

        minus.addActionListener(e -> {
            restaurant.removeItem(item);
            int q = restaurant.getItemQuantities().getOrDefault(item, 0);
            qty.setText(String.valueOf(q));
            refreshCart();
        });
        plus.addActionListener(e -> {
            restaurant.addItem(item);
            int q = restaurant.getItemQuantities().getOrDefault(item, 0);
            qty.setText(String.valueOf(q));
            refreshCart();
        });

        ctrl.add(minus);
        ctrl.add(qty);
        ctrl.add(plus);

        card.add(emojiBadge, BorderLayout.WEST);
        card.add(info, BorderLayout.CENTER);
        card.add(ctrl, BorderLayout.EAST);
        return card;
    }

    private JButton roundIconButton(String text, Color bg) {
        JButton btn = new JButton(text) {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                Graphics2D g2 = (Graphics2D) g.create();
                g2.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
                g2.setColor(getModel().isRollover() ? bg.brighter() : bg);
                g2.fillOval(0, 0, getWidth(), getHeight());
                g2.setColor(Color.WHITE);
                FontMetrics fm = g2.getFontMetrics();
                g2.drawString(getText(), (getWidth() - fm.stringWidth(getText())) / 2,
                        (getHeight() + fm.getAscent() - fm.getDescent()) / 2);
                g2.dispose();
            }
        };
        btn.setFont(UIHelper.font(Font.BOLD, 16));
        btn.setPreferredSize(new Dimension(30, 30));
        btn.setContentAreaFilled(false);
        btn.setBorderPainted(false);
        btn.setFocusPainted(false);
        btn.setCursor(Cursor.getPredefinedCursor(Cursor.HAND_CURSOR));
        return btn;
    }

    private void refreshCart() {
        cartPanel.removeAll();
        cartPanel.add(Box.createVerticalStrut(14));

        Map<String, Integer> quantities = restaurant.getItemQuantities();
        Map<String, Double> menu = restaurant.getMenuItems();
        Map<String, String> emojis = restaurant.getItemEmojis();

        if (quantities.isEmpty()) {
            JLabel empty = UIHelper.label("No items yet", UIHelper.font(Font.ITALIC, 13), UIHelper.MUTED);
            empty.setAlignmentX(Component.CENTER_ALIGNMENT);
            cartPanel.add(empty);
        } else {
            for (Map.Entry<String, Integer> entry : quantities.entrySet()) {
                JPanel row = buildCartRow(entry.getKey(), entry.getValue(),
                        menu.get(entry.getKey()), emojis.getOrDefault(entry.getKey(), "🍽️"));
                cartPanel.add(row);
                cartPanel.add(Box.createVerticalStrut(8));
            }
        }

        totalLabel.setText("Total:  Rs. " + String.format("%.0f", restaurant.getTotalAmount()));
        cartPanel.revalidate();
        cartPanel.repaint();
    }

    private JPanel buildCartRow(String item, int qty, double unitPrice, String emoji) {
        JPanel row = UIHelper.roundPanel(UIHelper.CARD, 10);
        row.setLayout(new BorderLayout(8, 0));
        row.setBorder(BorderFactory.createEmptyBorder(10, 12, 10, 12));
        row.setMaximumSize(new Dimension(Integer.MAX_VALUE, 58));

        JLabel lbl = UIHelper.label(emoji + "  " + item + " ×" + qty,
                UIHelper.font(Font.PLAIN, 13), UIHelper.TEXT);
        JLabel price = UIHelper.label("Rs. " + String.format("%.0f", unitPrice * qty),
                UIHelper.font(Font.BOLD, 13), restaurant.getAccentColor());

        row.add(lbl, BorderLayout.WEST);
        row.add(price, BorderLayout.EAST);
        return row;
    }
}

// ─────────────────────────────────────────────
//  RECEIPT SCREEN
// ─────────────────────────────────────────────
class ReceiptScreen extends JFrame {

    public ReceiptScreen(Restaurant r) {
        setTitle("Receipt — " + r.getName());
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(420, 560);
        setLocationRelativeTo(null);
        setResizable(false);
        UIHelper.styleFrame(this);

        JPanel root = new JPanel();
        root.setBackground(UIHelper.BG);
        root.setLayout(new BoxLayout(root, BoxLayout.Y_AXIS));
        root.setBorder(BorderFactory.createEmptyBorder(30, 30, 30, 30));

        // Header
        JLabel title = UIHelper.label("✅  Order Confirmed", UIHelper.font(Font.BOLD, 22), UIHelper.TEXT);
        title.setAlignmentX(Component.CENTER_ALIGNMENT);
        JLabel sub = UIHelper.label(r.getName() + "  •  Thank you!", UIHelper.font(Font.PLAIN, 13), UIHelper.MUTED);
        sub.setAlignmentX(Component.CENTER_ALIGNMENT);
        root.add(title);
        root.add(Box.createVerticalStrut(4));
        root.add(sub);
        root.add(Box.createVerticalStrut(24));

        // Divider
        root.add(divider());
        root.add(Box.createVerticalStrut(16));

        // Items
        Map<String, Integer> quantities = r.getItemQuantities();
        Map<String, Double> menu = r.getMenuItems();
        Map<String, String> emojis = r.getItemEmojis();
        for (Map.Entry<String, Integer> entry : quantities.entrySet()) {
            String item = entry.getKey();
            int qty = entry.getValue();
            double total = menu.get(item) * qty;

            JPanel row = new JPanel(new BorderLayout());
            row.setBackground(UIHelper.BG);
            row.setMaximumSize(new Dimension(Integer.MAX_VALUE, 30));
            String leftTxt = emojis.getOrDefault(item, "🍽️") + "  " + item + "  ×" + qty;
            row.add(UIHelper.label(leftTxt, UIHelper.font(Font.PLAIN, 13), UIHelper.TEXT), BorderLayout.WEST);
            row.add(UIHelper.label("Rs. " + String.format("%.0f", total), UIHelper.font(Font.BOLD, 13), UIHelper.TEXT), BorderLayout.EAST);
            root.add(row);
            root.add(Box.createVerticalStrut(8));
        }

        root.add(Box.createVerticalStrut(8));
        root.add(divider());
        root.add(Box.createVerticalStrut(16));

        // Subtotal / GST / Total
        double sub_amt = r.getTotalAmount();
        double gst = sub_amt * 0.18;
        double grand = sub_amt + gst;

        root.add(amountRow("Subtotal", sub_amt, UIHelper.MUTED));
        root.add(Box.createVerticalStrut(6));
        root.add(amountRow("GST (18%)", gst, UIHelper.MUTED));
        root.add(Box.createVerticalStrut(12));
        root.add(divider());
        root.add(Box.createVerticalStrut(14));
        root.add(amountRow("Grand Total", grand, r.getAccentColor()));

        root.add(Box.createVerticalStrut(28));

        // Done button
        JButton done = UIHelper.pillButton("Done", r.getAccentColor(),
                r.getName().equals("McDonald's") ? Color.BLACK : Color.WHITE, 10);
        done.setPreferredSize(new Dimension(300, 44));
        done.setMaximumSize(new Dimension(Integer.MAX_VALUE, 44));
        done.setAlignmentX(Component.CENTER_ALIGNMENT);
        done.addActionListener(e -> {
            dispose();
            new RestaurantSelection();
        });
        root.add(done);

        JScrollPane scroll = new JScrollPane(root);
        scroll.setBorder(null);
        scroll.getViewport().setBackground(UIHelper.BG);
        setContentPane(scroll);
        setVisible(true);
    }

    private JSeparator divider() {
        JSeparator sep = new JSeparator();
        sep.setForeground(UIHelper.BORDER);
        sep.setMaximumSize(new Dimension(Integer.MAX_VALUE, 1));
        return sep;
    }

    private JPanel amountRow(String label, double amount, Color valueColor) {
        JPanel row = new JPanel(new BorderLayout());
        row.setBackground(UIHelper.BG);
        row.setMaximumSize(new Dimension(Integer.MAX_VALUE, 28));
        int style = label.equals("Grand Total") ? Font.BOLD : Font.PLAIN;
        int size = label.equals("Grand Total") ? 15 : 13;
        row.add(UIHelper.label(label, UIHelper.font(style, size), UIHelper.MUTED), BorderLayout.WEST);
        row.add(UIHelper.label("Rs. " + String.format("%.2f", amount), UIHelper.font(Font.BOLD, size), valueColor), BorderLayout.EAST);
        return row;
    }
}

// ─────────────────────────────────────────────
//  RESTAURANT SELECTION SCREEN
// ─────────────────────────────────────────────
class RestaurantSelection extends JFrame {

    public RestaurantSelection() {
        setTitle("Choose Restaurant");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(560, 440);
        setLocationRelativeTo(null);
        setResizable(false);
        UIHelper.styleFrame(this);

        JPanel root = new JPanel();
        root.setBackground(UIHelper.BG);
        root.setLayout(new BoxLayout(root, BoxLayout.Y_AXIS));
        root.setBorder(BorderFactory.createEmptyBorder(36, 36, 36, 36));

        JLabel title = UIHelper.label("Where would you like to eat?", UIHelper.font(Font.BOLD, 22), UIHelper.TEXT);
        title.setAlignmentX(Component.CENTER_ALIGNMENT);
        JLabel sub = UIHelper.label("Select a restaurant to view its menu", UIHelper.font(Font.PLAIN, 13), UIHelper.MUTED);
        sub.setAlignmentX(Component.CENTER_ALIGNMENT);
        root.add(title);
        root.add(Box.createVerticalStrut(6));
        root.add(sub);
        root.add(Box.createVerticalStrut(30));

        Restaurant[] restaurants = {new McDonalds(), new Howdy(), new Ranchers()};
        for (Restaurant r : restaurants) {
            root.add(buildRestaurantCard(r));
            root.add(Box.createVerticalStrut(14));
        }

        setContentPane(root);
        setVisible(true);
    }

    private JPanel buildRestaurantCard(Restaurant r) {
        JPanel card = UIHelper.roundPanel(UIHelper.CARD, 16);
        card.setLayout(new BorderLayout(16, 0));
        card.setBorder(BorderFactory.createEmptyBorder(18, 20, 18, 20));
        card.setMaximumSize(new Dimension(Integer.MAX_VALUE, 80));
        card.setCursor(Cursor.getPredefinedCursor(Cursor.HAND_CURSOR));

        // Left: emoji in colored badge
        JLabel emojiLbl = new JLabel(r.getEmoji(), SwingConstants.CENTER);
        emojiLbl.setFont(new Font("Segoe UI Emoji", Font.PLAIN, 30));
        JPanel badge = UIHelper.roundPanel(r.getAccentColor().darker(), 12);
        badge.setPreferredSize(new Dimension(54, 54));
        badge.setLayout(new BorderLayout());
        badge.add(emojiLbl, BorderLayout.CENTER);

        // Center: name + tagline
        JPanel info = new JPanel();
        info.setOpaque(false);
        info.setLayout(new BoxLayout(info, BoxLayout.Y_AXIS));
        JLabel name = UIHelper.label(r.getName(), UIHelper.font(Font.BOLD, 16), UIHelper.TEXT);
        int items = r.getMenuItems().size();
        JLabel count = UIHelper.label(items + " items on menu", UIHelper.font(Font.PLAIN, 12), UIHelper.MUTED);
        info.add(name);
        info.add(Box.createVerticalStrut(3));
        info.add(count);

        // Right: arrow
        JLabel arrow = UIHelper.label("›", UIHelper.font(Font.BOLD, 24), UIHelper.MUTED);

        card.add(badge, BorderLayout.WEST);
        card.add(info, BorderLayout.CENTER);
        card.add(arrow, BorderLayout.EAST);

        // Hover effect
        card.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseEntered(MouseEvent e) {
                card.repaint();
                arrow.setForeground(r.getAccentColor());
            }

            @Override
            public void mouseExited(MouseEvent e) {
                arrow.setForeground(UIHelper.MUTED);
            }

            @Override
            public void mouseClicked(MouseEvent e) {
                dispose();
                new OrderScreen(r);
            }
        });

        return card;
    }
}

// ─────────────────────────────────────────────
//  LOGIN SCREEN
// ─────────────────────────────────────────────
class Login extends JFrame {

    private static final String USERNAME = "project";
    private static final String PASSWORD = "password";

    public Login() {
        setTitle("Food Ordering — Login");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(400, 480);
        setLocationRelativeTo(null);
        setResizable(false);
        UIHelper.styleFrame(this);

        JPanel root = new JPanel();
        root.setBackground(UIHelper.BG);
        root.setLayout(new BoxLayout(root, BoxLayout.Y_AXIS));
        root.setBorder(BorderFactory.createEmptyBorder(50, 40, 40, 40));

        // Logo area
        JLabel logoEmoji = new JLabel("🍽️", SwingConstants.CENTER);
        logoEmoji.setFont(new Font("Segoe UI Emoji", Font.PLAIN, 52));
        logoEmoji.setAlignmentX(Component.CENTER_ALIGNMENT);
        root.add(logoEmoji);
        root.add(Box.createVerticalStrut(16));

        JLabel title = UIHelper.label("Welcome Back", UIHelper.font(Font.BOLD, 26), UIHelper.TEXT);
        title.setAlignmentX(Component.CENTER_ALIGNMENT);
        JLabel sub = UIHelper.label("Sign in to start ordering", UIHelper.font(Font.PLAIN, 14), UIHelper.MUTED);
        sub.setAlignmentX(Component.CENTER_ALIGNMENT);
        root.add(title);
        root.add(Box.createVerticalStrut(4));
        root.add(sub);
        root.add(Box.createVerticalStrut(36));

        // Username field
        root.add(fieldLabel("Username"));
        root.add(Box.createVerticalStrut(6));
        JTextField usernameField = styledField(false);
        root.add(usernameField);
        root.add(Box.createVerticalStrut(16));

        // Password field
        root.add(fieldLabel("Password"));
        root.add(Box.createVerticalStrut(6));
        JPasswordField passwordField = (JPasswordField) styledField(true);
        root.add(passwordField);
        root.add(Box.createVerticalStrut(28));

        // Error label
        JLabel errorLabel = UIHelper.label("", UIHelper.font(Font.PLAIN, 12), new Color(255, 80, 80));
        errorLabel.setAlignmentX(Component.CENTER_ALIGNMENT);
        root.add(errorLabel);
        root.add(Box.createVerticalStrut(8));

        // Login button
        JButton loginBtn = UIHelper.pillButton("Sign In", new Color(255, 188, 0), Color.BLACK, 10);
        loginBtn.setPreferredSize(new Dimension(300, 46));
        loginBtn.setMaximumSize(new Dimension(Integer.MAX_VALUE, 46));
        loginBtn.setAlignmentX(Component.CENTER_ALIGNMENT);
        loginBtn.setFont(UIHelper.font(Font.BOLD, 15));
        root.add(loginBtn);

        // Hint
        root.add(Box.createVerticalStrut(18));
        JLabel hint = UIHelper.label("Default: project / password", UIHelper.font(Font.ITALIC, 11), UIHelper.MUTED);
        hint.setAlignmentX(Component.CENTER_ALIGNMENT);
        root.add(hint);

        loginBtn.addActionListener(e -> {
            String u = usernameField.getText().trim();
            String p = new String(passwordField.getPassword()).trim();
            if (USERNAME.equals(u) && PASSWORD.equals(p)) {
                dispose();
                new RestaurantSelection();
            } else {
                errorLabel.setText("⚠  Incorrect username or password");
                passwordField.setText("");
            }
        });

        // Enter key support
        ActionListener loginAction = loginBtn.getActionListeners()[0];
        usernameField.addActionListener(loginAction);
        passwordField.addActionListener(loginAction);

        setContentPane(root);
        setVisible(true);
    }

    private JLabel fieldLabel(String text) {
        JLabel l = UIHelper.label(text, UIHelper.font(Font.BOLD, 12), UIHelper.MUTED);
        l.setAlignmentX(Component.CENTER_ALIGNMENT);
        return l;
    }

    private JTextField styledField(boolean isPassword) {
        JTextField field = isPassword ? new JPasswordField() : new JTextField();
        field.setFont(UIHelper.font(Font.PLAIN, 14));
        field.setForeground(UIHelper.TEXT);
        field.setBackground(UIHelper.CARD);
        field.setCaretColor(UIHelper.TEXT);
        field.setBorder(BorderFactory.createCompoundBorder(
                BorderFactory.createLineBorder(UIHelper.BORDER, 1),
                BorderFactory.createEmptyBorder(10, 14, 10, 14)));
        field.setMaximumSize(new Dimension(Integer.MAX_VALUE, 46));

        // Focus border highlight
        field.addFocusListener(new FocusAdapter() {
            @Override
            public void focusGained(FocusEvent e) {
                field.setBorder(BorderFactory.createCompoundBorder(
                        BorderFactory.createLineBorder(new Color(255, 188, 0), 1),
                        BorderFactory.createEmptyBorder(10, 14, 10, 14)));
            }

            @Override
            public void focusLost(FocusEvent e) {
                field.setBorder(BorderFactory.createCompoundBorder(
                        BorderFactory.createLineBorder(UIHelper.BORDER, 1),
                        BorderFactory.createEmptyBorder(10, 14, 10, 14)));
            }
        });
        return field;
    }
}

// ─────────────────────────────────────────────
//  MAIN
// ─────────────────────────────────────────────
public class Application {

    public static void main(String[] args) {
        // Use system look on Windows, keep dark custom on others
        try {
            UIManager.setLookAndFeel(UIManager.getCrossPlatformLookAndFeelClassName());
        } catch (Exception ignored) {
        }

        SwingUtilities.invokeLater(Login::new);
    }
}
