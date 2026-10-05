(function () {
  "use strict";

  function initRKFrames() {
    document.getElementById("year").textContent = new Date().getFullYear();

    const categoryButtons = document.querySelectorAll(".category-btn");
    const productCards = document.querySelectorAll(".product-card");

    categoryButtons.forEach((btn) => {
      btn.addEventListener("click", () => {
        categoryButtons.forEach((b) => b.classList.remove("active"));
        btn.classList.add("active");
        const category = btn.dataset.category;

        productCards.forEach((card) => {
          const show = category === "all" || card.dataset.category === category;
          card.style.display = show ? "" : "none";
        });
      });
    });
    const FRAME_SIZES = [
      { w: 20, h: 30, label: "20×30cm" },
      { w: 30, h: 40, label: "30×40cm" },
      { w: 40, h: 60, label: "40×60cm" },
    ];
    const PX_PER_CM = 12; // canvas scale factor

    let selectedSize = FRAME_SIZES[0];
    let selectedColor = "#1a1a1a";
    let selectedMat = "#f5f2ea";
    let frameWidth = 10;
    let matWidth = 10;
    let uploadedImage = null; // HTMLImageElement

    const canvas = document.getElementById("previewCanvas");
    const ctx = canvas.getContext("2d");
    const downloadBtn = document.getElementById("downloadBtn");

    document.querySelectorAll(".size-btn").forEach((btn) => {
      btn.addEventListener("click", () => {
        document
          .querySelectorAll(".size-btn")
          .forEach((b) => b.classList.remove("active"));
        btn.classList.add("active");
        selectedSize = { w: Number(btn.dataset.w), h: Number(btn.dataset.h) };
        checkSizeFit();
        drawPreview();
      });
    });

    document.querySelectorAll(".swatch").forEach((btn) => {
      btn.addEventListener("click", () => {
        document
          .querySelectorAll(".swatch")
          .forEach((b) => b.classList.remove("active"));
        btn.classList.add("active");
        selectedColor = btn.dataset.color;
        selectedMat = btn.dataset.mat;
        drawPreview();
      });
    });

    document
      .getElementById("frameWidthRange")
      .addEventListener("input", (e) => {
        frameWidth = Number(e.target.value);
        drawPreview();
      });
    document.getElementById("matWidthRange").addEventListener("input", (e) => {
      matWidth = Number(e.target.value);
      drawPreview();
    });

    /* ---------------- PHOTO UPLOAD + SIZE-FIT CHECK ---------------- */
    document.getElementById("photoInput").addEventListener("change", (e) => {
      const file = e.target.files[0];
      if (!file) return;

      const reader = new FileReader();
      reader.onload = (ev) => {
        const img = new Image();
        img.onload = () => {
          uploadedImage = img;
          checkSizeFit();
          drawPreview();
          downloadBtn.disabled = false;
          const customOrderBtn = document.getElementById("custom-add-to-cart-btn");
          if (customOrderBtn) customOrderBtn.disabled = false;
        };
        img.src = ev.target.result;
      };
      reader.readAsDataURL(file);
    });
    function checkSizeFit() {
      if (!uploadedImage) return;

      // Normalize to a "short side / long side" ratio so orientation doesn't matter.
      const imgRatio =
        Math.min(uploadedImage.width, uploadedImage.height) /
        Math.max(uploadedImage.width, uploadedImage.height);

      let bestDiff = Infinity;
      let bestSizes = [];
      FRAME_SIZES.forEach((size) => {
        const sizeRatio = Math.min(size.w, size.h) / Math.max(size.w, size.h);
        const diff = Math.abs(sizeRatio - imgRatio);
        if (diff < bestDiff - 0.001) {
          bestDiff = diff;
          bestSizes = [size];
        } else if (Math.abs(diff - bestDiff) <= 0.001) {
          bestSizes.push(size);
        }
      });

      const selectedRatio =
        Math.min(selectedSize.w, selectedSize.h) /
        Math.max(selectedSize.w, selectedSize.h);
      const selectedDiff = Math.abs(selectedRatio - imgRatio);

      const THRESHOLD = 0.06; // tweak sensitivity here
      const alreadyBest = bestSizes.some(
        (s) => s.w === selectedSize.w && s.h === selectedSize.h,
      );

      if (!alreadyBest && selectedDiff > THRESHOLD) {
        showSizeWarning(bestSizes);
      }
    }
    function drawPreview() {
      const width = selectedSize.w * PX_PER_CM;
      const height = selectedSize.h * PX_PER_CM;
      canvas.width = width;
      canvas.height = height;

      ctx.clearRect(0, 0, width, height);

      // outer frame with a subtle drop shadow
      ctx.save();
      ctx.shadowColor = "rgba(0,0,0,0.25)";
      ctx.shadowBlur = 30;
      ctx.shadowOffsetY = 12;
      ctx.fillStyle = selectedColor;
      ctx.fillRect(0, 0, width, height);
      ctx.restore();

      // bevel line
      ctx.strokeStyle = "rgba(0,0,0,0.25)";
      ctx.lineWidth = 2;
      ctx.strokeRect(
        frameWidth * 0.4,
        frameWidth * 0.4,
        width - frameWidth * 0.8,
        height - frameWidth * 0.8,
      );

      // mat board
      const matX = frameWidth;
      const matY = frameWidth;
      const matW = width - frameWidth * 2;
      const matH = height - frameWidth * 2;
      ctx.fillStyle = selectedMat;
      ctx.fillRect(matX, matY, matW, matH);

      // photo opening
      const openX = matX + matWidth;
      const openY = matY + matWidth;
      const openW = matW - matWidth * 2;
      const openH = matH - matWidth * 2;

      if (openW <= 0 || openH <= 0) return; // frame/mat too thick for this canvas size

      ctx.save();
      ctx.shadowColor = "rgba(0,0,0,0.35)";
      ctx.shadowBlur = 10;
      ctx.fillStyle = "#000";
      ctx.fillRect(openX, openY, openW, openH);
      ctx.restore();

      if (uploadedImage) {
        const targetRatio = openW / openH;
        const imgRatio = uploadedImage.width / uploadedImage.height;
        let sx, sy, sw, sh;
        if (imgRatio > targetRatio) {
          sh = uploadedImage.height;
          sw = sh * targetRatio;
          sx = (uploadedImage.width - sw) / 2;
          sy = 0;
        } else {
          sw = uploadedImage.width;
          sh = sw / targetRatio;
          sx = 0;
          sy = (uploadedImage.height - sh) / 2;
        }
        ctx.drawImage(
          uploadedImage,
          sx,
          sy,
          sw,
          sh,
          openX,
          openY,
          openW,
          openH,
        );
      } else {
        ctx.fillStyle = "#888";
        ctx.font = "16px sans-serif";
        ctx.textAlign = "center";
        ctx.fillText(
          "Upload a photo to preview it here",
          openX + openW / 2,
          openY + openH / 2,
        );
      }
    }
    downloadBtn.addEventListener("click", () => {
      const link = document.createElement("a");
      link.download = `rk-frames-preview-${selectedSize.w}x${selectedSize.h}.png`;
      link.href = canvas.toDataURL("image/png");
      link.click();
    });

    /* initial render */
    drawPreview();

    // EmailJS settings.

    const EMAILJS_SERVICE_ID = "service_3knosym";
    const EMAILJS_TEMPLATE_ID = "template_b0tiy9h";

    const RK_CART_KEY = "rk-frames-cart";

    const rkMessageModal = document.getElementById("rk-message-modal");
    const rkMessageText = document.getElementById("rk-message-text");
    const rkMessageTitle = document.getElementById("rk-message-title");

    function rkShowPopup(message, title = "Notice") {
      if (!rkMessageModal || !rkMessageText) {
        console.error(message);
        return;
      }

      if (rkMessageTitle) rkMessageTitle.textContent = title;
      rkMessageText.innerHTML = message;
      rkMessageModal.classList.add("open");
    }

    function rkClosePopup() {
      rkMessageModal?.classList.remove("open");
    }

    // Alias used by the size-fit check.
    function showRKPopup(message) {
      rkShowPopup(message, "Size Notice");
    }

    document
      .getElementById("close-rk-message")
      ?.addEventListener("click", rkClosePopup);
    document
      .getElementById("rk-message-ok")
      ?.addEventListener("click", rkClosePopup);

    rkMessageModal?.addEventListener("click", (event) => {
      if (event.target === rkMessageModal) rkClosePopup();
    });

    let recommendedSize = null;
    const sizeWarningModal = document.getElementById("size-warning-modal");
    const sizeWarningText = document.getElementById("size-warning-text");
    const useRecommendedSizeBtn = document.getElementById(
      "use-recommended-size",
    );
    const keepSelectedSizeBtn = document.getElementById("keep-selected-size");
    const closeSizeWarningBtn = document.getElementById("close-size-warning");

    function showSizeWarning(bestSizes) {
      if (!sizeWarningModal || !sizeWarningText) return;

      recommendedSize = bestSizes[0];
      const bestLabel = bestSizes.map((size) => size.label).join(" or ");
      const selectedLabel =
        selectedSize.label || `${selectedSize.w}×${selectedSize.h}cm`;

      sizeWarningText.innerHTML =
        `This photo may require significant cropping in <strong>${rkEscapeHTML(selectedLabel)}</strong>.<br><br>` +
        `Recommended size: <strong>${rkEscapeHTML(bestLabel)}</strong>`;

      sizeWarningModal.classList.add("open");
    }

    function closeSizeWarning() {
      sizeWarningModal?.classList.remove("open");
    }

    closeSizeWarningBtn?.addEventListener("click", closeSizeWarning);
    keepSelectedSizeBtn?.addEventListener("click", closeSizeWarning);

    useRecommendedSizeBtn?.addEventListener("click", () => {
      if (!recommendedSize) return;

      selectedSize = recommendedSize;

      document.querySelectorAll(".size-btn").forEach((btn) => {
        const matches =
          Number(btn.dataset.w) === recommendedSize.w &&
          Number(btn.dataset.h) === recommendedSize.h;
        btn.classList.toggle("active", matches);
      });

      closeSizeWarning();
      drawPreview();
    });

    sizeWarningModal?.addEventListener("click", (event) => {
      if (event.target === sizeWarningModal) closeSizeWarning();
    });

    function rkProductImage(id) {
      const card = document.querySelector(
        `.product-card[data-id="${CSS.escape(id)}"]`,
      );
      return card?.querySelector("img.poster")?.getAttribute("src") || "";
    }

    // Load saved cart safely
    function loadRKCart() {
      try {
        const saved = JSON.parse(localStorage.getItem(RK_CART_KEY) || "[]");
        return Array.isArray(saved)
          ? saved
              .filter(
                (item) =>
                  item &&
                  typeof item.id === "string" &&
                  typeof item.name === "string" &&
                  Number.isFinite(Number(item.price)) &&
                  Number(item.price) >= 0 &&
                  Number.isInteger(Number(item.quantity)) &&
                  Number(item.quantity) > 0,
              )
              .map((item) => ({
                ...item,
                image: item.image || rkProductImage(item.id),
                price: Number(item.price),
                quantity: Number(item.quantity),
              }))
          : [];
      } catch {
        return [];
      }
    }

    let rkCart = loadRKCart();

    // Elements
    const rkCartModal = document.getElementById("cart-modal");
    const rkCheckoutModal = document.getElementById("checkout-modal");
    const rkCartItems = document.getElementById("cart-items");
    const rkCartCount = document.getElementById("cart-count");
    const rkSubtotal = document.getElementById("cart-subtotal");
    const rkTotal = document.getElementById("cart-total");
    const rkCheckoutItems = document.getElementById("checkout-items");
    const rkCheckoutTotal = document.getElementById("checkout-total");
    const rkCheckoutForm = document.getElementById("checkout-form");

    document
      .getElementById("close-order-success")
      ?.addEventListener("click", () => {
        document
          .getElementById("order-success-modal")
          ?.classList.remove("open");
      });

    document
      .getElementById("order-success-modal")
      ?.addEventListener("click", (event) => {
        if (event.target.id === "order-success-modal") {
          event.currentTarget.classList.remove("open");
        }
      });

    // Currency formatter
    function rkMoney(amount) {
      return `${Number(amount).toLocaleString("en-EG")} LE`;
    }

    // Calculate cart totals
    function rkCartSubtotal() {
      return rkCart.reduce((sum, item) => sum + item.price * item.quantity, 0);
    }

    function rkSaveCart() {
      try {
        localStorage.setItem(RK_CART_KEY, JSON.stringify(rkCart));
      } catch (error) {
        console.warn("Could not save cart:", error);
      }
      rkRenderCart();
    }

    // Create elements safely
    function rkElement(tag, className, text) {
      const element = document.createElement(tag);
      if (className) element.className = className;
      if (text !== undefined) element.textContent = text;
      return element;
    }

    /* ---------------- PRODUCT OPTIONS + ADD TO CART ---------------- */
    const productCardsForOptions = document.querySelectorAll(".product-card");

    productCardsForOptions.forEach((card) => {
      const sizeSelect = card.querySelector(".product-size");
      const colorButtons = card.querySelectorAll(".product-color");
      const priceEl = card.querySelector(".product-price");

      function updateProductPrice() {
        if (!sizeSelect || !priceEl) return;
        const option = sizeSelect.options[sizeSelect.selectedIndex];
        const price = Number(option?.dataset.price || card.dataset.price || 0);
        priceEl.textContent = rkMoney(price);
      }

      sizeSelect?.addEventListener("change", updateProductPrice);

      colorButtons.forEach((colorButton) => {
        colorButton.addEventListener("click", () => {
          colorButtons.forEach((button) => button.classList.remove("active"));
          colorButton.classList.add("active");
        });
      });

      updateProductPrice();
    });

    document
      .querySelectorAll(".product-card .add-to-cart")
      .forEach((button) => {
        button.addEventListener("click", () => {
          const card = button.closest(".product-card");
          if (!card) return;

          const baseId = card.dataset.id;
          const baseName =
            card.dataset.name || card.querySelector("h3")?.textContent.trim();
          const category = card.dataset.category || "";
          const image =
            card.querySelector("img.poster")?.getAttribute("src") || "";
          const sizeSelect = card.querySelector(".product-size");
          const selectedOption = sizeSelect?.options[sizeSelect.selectedIndex];
          const size = selectedOption?.value || "20×30cm";
          const price = Number(
            selectedOption?.dataset.price || card.dataset.price || 350,
          );
          const activeColor = card.querySelector(
            ".product-color.active",
          );
          const color = activeColor?.dataset.color || "Black Wood";

          if (!baseId || !baseName || !Number.isFinite(price)) {
            rkShowPopup(
              "This product is missing its ID, name or valid price.",
              "Product Error",
            );
            return;
          }

          const id = `${baseId}__${size}__${color}`;
          const name = `${baseName} — ${size} — ${color}`;
          const existing = rkCart.find((item) => item.id === id);

          if (existing) {
            existing.quantity += 1;
          } else {
            rkCart.push({
              id,
              baseId,
              name,
              price,
              category,
              image,
              size,
              color,
              quantity: 1,
            });
          }

          rkSaveCart();

          const originalText = button.textContent;
          button.textContent = "Added ✓";
          button.disabled = true;

          setTimeout(() => {
            button.textContent = originalText;
            button.disabled = false;
          }, 900);
        });
      });

    function rkRenderCart() {
      const totalQuantity = rkCart.reduce(
        (sum, item) => sum + item.quantity,
        0,
      );

      const subtotal = rkCartSubtotal();

      rkCartCount.textContent = totalQuantity;
      rkSubtotal.textContent = rkMoney(subtotal);
      rkTotal.textContent = rkMoney(subtotal);

      rkCartItems.replaceChildren();

      if (rkCart.length === 0) {
        const empty = rkElement(
          "p",
          "empty-cart",
          "Your cart is empty. Browse our posters and add your favorites!",
        );
        rkCartItems.appendChild(empty);
        return;
      }

      rkCart.forEach((item) => {
        const row = rkElement("div", "cart-item");
        const imageWrap = rkElement("div", "cart-item-image");
        const details = rkElement("div", "cart-item-details");

        if (item.image) {
          const image = document.createElement("img");
          image.src = item.image;
          image.alt = item.name;
          image.loading = "lazy";
          imageWrap.appendChild(image);
        }

        const name = rkElement("strong", "", item.name);
        const unitPrice = rkElement("p", "", `${rkMoney(item.price)} each`);
        const quantityControls = rkElement("div", "cart-quantity");

        const decrease = rkElement("button", "", "−");
        decrease.type = "button";
        decrease.setAttribute("aria-label", `Decrease ${item.name}`);

        const quantity = rkElement("span", "", String(item.quantity));
        quantity.setAttribute("aria-live", "polite");

        const increase = rkElement("button", "", "+");
        increase.type = "button";
        increase.setAttribute("aria-label", `Increase ${item.name}`);

        const lineTotal = rkElement(
          "p",
          "cart-line-total",
          `Item total: ${rkMoney(item.price * item.quantity)}`,
        );

        const remove = rkElement("button", "remove-item", "Remove");
        remove.type = "button";

        decrease.addEventListener("click", () => {
          item.quantity -= 1;
          if (item.quantity <= 0) {
            rkCart = rkCart.filter((product) => product.id !== item.id);
          }
          rkSaveCart();
        });

        increase.addEventListener("click", () => {
          item.quantity += 1;
          rkSaveCart();
        });

        remove.addEventListener("click", () => {
          rkCart = rkCart.filter((product) => product.id !== item.id);
          rkSaveCart();
        });

        quantityControls.append(decrease, quantity, increase);
        details.append(name, unitPrice, quantityControls, lineTotal, remove);
        row.append(imageWrap, details);
        rkCartItems.appendChild(row);
      });
    }

    document.getElementById("cart-toggle").addEventListener("click", () => {
      rkRenderCart();
      rkCartModal.classList.add("open");
    });

    document.getElementById("close-cart").addEventListener("click", () => {
      rkCartModal.classList.remove("open");
    });

    function rkRenderCheckout() {
      rkCheckoutItems.replaceChildren();

      rkCart.forEach((item) => {
        const row = rkElement("div", "checkout-item");
        const imageWrap = rkElement("div", "checkout-item-image");
        const info = rkElement("div", "checkout-item-info");

        if (item.image) {
          const image = document.createElement("img");
          image.src = item.image;
          image.alt = item.name;
          image.loading = "lazy";
          imageWrap.appendChild(image);
        }

        const product = rkElement(
          "span",
          "checkout-item-name",
          `${item.name} × ${item.quantity}`,
        );
        const price = rkElement(
          "strong",
          "",
          rkMoney(item.price * item.quantity),
        );

        info.append(product, price);
        row.append(imageWrap, info);
        rkCheckoutItems.appendChild(row);
      });

      rkCheckoutTotal.textContent = rkMoney(rkCartSubtotal());
    }

    document.getElementById("checkout-btn").addEventListener("click", () => {
      if (rkCart.length === 0) {
        rkShowPopup("Your cart is empty.", "Your Cart");
        return;
      }

      rkRenderCheckout();
      rkCartModal.classList.remove("open");
      rkCheckoutModal.classList.add("open");
    });

    document.getElementById("close-checkout").addEventListener("click", () => {
      rkCheckoutModal.classList.remove("open");
    });

    document.getElementById("back-to-cart").addEventListener("click", () => {
      rkCheckoutModal.classList.remove("open");
      rkCartModal.classList.add("open");
    });

    function rkEscapeHTML(value) {
      return String(value).replace(
        /[&<>"']/g,
        (char) =>
          ({
            "&": "&amp;",
            "<": "&lt;",
            ">": "&gt;",
            '"': "&quot;",
            "'": "&#39;",
          })[char],
      );
    }

    rkCheckoutForm.addEventListener("submit", async (event) => {
      event.preventDefault();

      if (rkCart.length === 0) {
        rkCheckoutModal.classList.remove("open");
        rkShowPopup("Your cart is empty.", "Your Cart");
        return;
      }

      const name = document.getElementById("customer-name")?.value.trim() || "";
      const phone =
        document.getElementById("customer-phone")?.value.trim() || "";
      const address =
        document.getElementById("customer-address")?.value.trim() || "";
      const notes =
        document.getElementById("customer-notes")?.value.trim() || "";

      if (!name || !phone || !address) {
        rkShowPopup(
          "Please fill in all required delivery details.",
          "Missing Details",
        );
        return;
      }

      if (!window.emailjs) {
        rkShowPopup(
          "Email service is not loaded. Please check your internet connection and try again.",
          "Email Error",
        );
        return;
      }

      if (
        EMAILJS_SERVICE_ID === "YOUR_EMAILJS_SERVICE_ID" ||
        EMAILJS_TEMPLATE_ID === "YOUR_EMAILJS_TEMPLATE_ID"
      ) {
        rkShowPopup(
          "EmailJS is not configured yet. Add your Service ID and Template ID to <strong>script.js</strong> first.",
          "EmailJS Setup Required",
        );
        return;
      }

      const placeOrderBtn = document.getElementById("place-order-btn");
      const originalButtonText = placeOrderBtn?.textContent || "Place Order";

      if (placeOrderBtn) {
        placeOrderBtn.disabled = true;
        placeOrderBtn.textContent = "Sending Order...";
      }

      const order = {
        id: "RK-" + Date.now().toString().slice(-8),
        date: new Date().toLocaleString("en-EG"),
        name,
        phone,
        address,
        notes,
        items: rkCart.map((item) => ({ ...item })),
        total: rkCartSubtotal(),
      };

      const orderItems = order.items
        .map((item, index) => {
          const imageURL = item.image
            ? new URL(item.image, window.location.href).href
            : "";

          return [
            `${index + 1}. ${item.name}`,
            `   Quantity: ${item.quantity}`,
            `   Unit Price: ${rkMoney(item.price)}`,
            `   Subtotal: ${rkMoney(item.price * item.quantity)}`,
            imageURL ? `   Poster: ${imageURL}` : "",
          ]
            .filter(Boolean)
            .join("\n");
        })
        .join("\n\n");

      // Build email items with an image CID for every unique product in the order.
      // EmailJS will attach these images and they can also be displayed directly
      // inside the email using <img src="cid:product_image_0">, etc.
      const MAX_EMAIL_IMAGES = 10;
      const emailItems = order.items.slice(0, MAX_EMAIL_IMAGES).map((item, index) => ({
        name: item.name,
        units: item.quantity || item.units || 1,
        price: `${Number(item.price || 0).toFixed(2)} EGP`,
        image_url: item.image ? `cid:product_image_${index}` : "",
      }));

      const templateParams = {
        order_id: order.id,
        order_date: order.date,
        customer_name: order.name,
        customer_phone: order.phone,
        customer_address: order.address,
        customer_notes: order.notes || "No additional notes",
        orders: emailItems,
        total: `${Number(order.total || 0).toFixed(2)} EGP`,
      };

      // Add every product/custom-frame image as a separate EmailJS attachment
      // variable. The EmailJS template must have matching Variable Attachments
      // named product_image_0 through product_image_9.
      order.items.slice(0, MAX_EMAIL_IMAGES).forEach((item, index) => {
        if (item.image) {
          templateParams[`product_image_${index}`] = item.image;
        }
      });

      try {
        // Wait for EmailJS to actually send the order before confirming it.
        const response = await emailjs.send(
          EMAILJS_SERVICE_ID,
          EMAILJS_TEMPLATE_ID,
          templateParams
        );

        console.log("Order email sent:", response.status, response.text);

        // No client-side PDF/receipt window.
        rkCheckoutModal.classList.remove("open");
        rkCart = [];
        rkSaveCart();
        rkCheckoutForm.reset();

        const successModal = document.getElementById("order-success-modal");
        successModal?.classList.add("open");
      } catch (error) {
        console.error("EmailJS order failed:", error);

        const errorMessage =
          error?.text ||
          error?.message ||
          "The order could not be sent. Please try again.";

        rkShowPopup(
          `<strong>Order could not be sent.</strong><br><br>${rkEscapeHTML(errorMessage)}`,
          "Order Error",
        );
      } finally {
        if (placeOrderBtn) {
          placeOrderBtn.disabled = false;
          placeOrderBtn.textContent = originalButtonText;
        }
      }
    });

    [rkCartModal, rkCheckoutModal].forEach((modal) => {
      modal.addEventListener("click", (event) => {
        if (event.target === modal) {
          modal.classList.remove("open");
        }
      });
    });

    document.addEventListener("keydown", (event) => {
      if (event.key === "Escape") {
        rkCartModal.classList.remove("open");
        rkCheckoutModal.classList.remove("open");
        rkMessageModal?.classList.remove("open");
        document.getElementById("size-warning-modal")?.classList.remove("open");
        document
          .getElementById("order-success-modal")
          ?.classList.remove("open");
      }
    });

    /* ---------------- CUSTOM FRAME ORDER ---------------- */
    const customOrderBtn = document.getElementById("custom-add-to-cart-btn");

    customOrderBtn?.addEventListener("click", () => {
      if (!uploadedImage) {
        rkShowPopup("Please upload a photo first.", "Custom Frame");
        return;
      }

      const sizeLabel = selectedSize.label || `${selectedSize.w}×${selectedSize.h}cm`;
      const colorName = selectedColor === "#ffffff" ? "Classic White" : "Black Wood";
      const priceMap = {
        "20×30cm": 350,
        "30×40cm": 450,
        "40×60cm": 600,
      };
      const price = priceMap[sizeLabel] || 350;
      const id = `custom-frame__${sizeLabel}__${colorName}`;

      const existing = rkCart.find((item) => item.id === id);
      if (existing) {
        existing.quantity += 1;
      } else {
        rkCart.push({
          id,
          name: `Custom Photo Frame — ${sizeLabel} — ${colorName}`,
          price,
          category: "Custom-Design",
          image: canvas.toDataURL("image/jpeg", 0.72),
          size: sizeLabel,
          color: colorName,
          custom: true,
          quantity: 1,
        });
      }

      rkSaveCart();
      rkRenderCheckout();
      rkCartModal.classList.remove("open");
      rkCheckoutModal.classList.add("open");
    });

    // Initial render
    rkRenderCart();
  }

  if (document.readyState === "loading") {
    document.addEventListener("DOMContentLoaded", initRKFrames, { once: true });
  } else {
    initRKFrames();
  }
})();
