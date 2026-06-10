# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-10T11:40:01.789049+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×70 (24h) → ログ/DB確認

### 検出された問題
- 🔴 CIRCUIT_BREAKER_TRIP×70 (24h)
- 🔴 CALIBRATION_DRIFT×35 (24h)
- 🟡 FINAL_MISSING×22 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-10T11:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-10T11:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-06-10T11:30:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S02_TETSUBAN が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CALIBRATION_DRIFT  ×37  [2026-06-10T11:02:30]
- key: `CALIBRATION_DRIFT|`
- **FIX**: 予測確率が実的中率から50%以上乖離→isotonic_calibration.json 再生成 or モデル再学習が必要。EV計算が膨張中

### 🔴 CIRCUIT_BREAKER_TRIP  ×111  [2026-06-10T11:02:30]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×111  [2026-06-10T11:02:30]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-06-10T11:02:30]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-10T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=83<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-10T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=37 hit%=27.0% ROI=1.00 (コスト 8,400/回収 8,380)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-10T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1254 actual=0.1667 gap=-0.0412`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-10T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=6 pred=0.2216 actual=0.3333 gap=-0.1117`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-10T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1918 actual=0.2000 gap=-0.0082`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-10T06:00:13]
- key: `ROI_STAT|S00: n=153 hit%=25.5% hit_CI[Bonf]=[16.8,36.7]% ROI=0.78 ROI_boot95=[0.53,1.07]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-10T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=153<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-10T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=143 hit%=28.7% hit_CI[Bonf]=[19.2,40.5]% ROI=0.70 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-10T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=143<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-10T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=83 hit%=39.8% hit_CI[Bonf]=[25.9,55.5]% ROI=0.68 ROI_boot95=[0.4`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-06-10T06:00:13]
- key: `ORPHAN_SCAN|142 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-10T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=35 hit%=31.4% ROI=0.86 (コスト 10,300/回収 8,880)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-10T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=36 hit%=22.2% ROI=0.47 (コスト 7,900/回収 3,690)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.78MB / last modified 2026-06-10T11:39:27.880841+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
=== run_cycle 11:38:06 ===
2026-06-10 11:38:06,233 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-10 11:38:06,233 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-10 11:38:06,277 [INFO] predictor: Models loaded OK
2026-06-10 11:38:06,372 [INFO] run_cycle: run_cycle done: 0 notifications
2026-06-10 11:39:05,870 [INFO] run_cycle: === run_cycle 11:39:05 ===
2026-06-10 11:39:05,870 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-06-10 11:39:05,870 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-06-10 11:39:05,916 [INFO] predictor: Models loaded OK
2026-06-10 11:39:17,304 [INFO] scraper: odds3t: 120/120 parsed
2026-06-10 11:39:18,457 [INFO] scraper: odds3f: 20/20 parsed
2026-06-10 11:39:19,555 [INFO] scraper: odds2t: 30/30 parsed
2026-06-10 11:39:19,556 [INFO] scraper: odds2f: 14/15 parsed
2026-06-10 11:39:20,760 [INFO] scraper: odds_win: 6/6 parsed
2026-06-10 11:39:20,760 [INFO] scraper: fetch_race 23/8: boats=6 odds=190/191
2026-06-10 11:39:20,764 [INFO] predictor: CALIBRATION_MODE=on
2026-06-10 11:39:20,764 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-06-10 11:39:20,768 [INFO] run_cycle: fetched 23/8 [scan]: 156 combos
2026-06-10 11:39:24,359 [INFO] scraper: odds3t: 120/120 parsed
2026-06-10 11:39:25,452 [INFO] scraper: odds3f: 20/20 parsed
2026-06-10 11:39:26,543 [INFO] scraper: odds2t: 26/30 parsed
2026-06-10 11:39:26,544 [INFO] scraper: odds2f: 12/15 parsed
2026-06-10 11:39:27,618 [INFO] scraper: odds_win: 3/6 parsed
2026-06-10 11:39:27,618 [INFO] scraper: fetch_race 11/4: boats=6 odds=181/191
2026-06-10 11:39:27,621 [INFO] predictor: CALIBRATION_MODE=on
2026-06-10 11:39:27,621 [INFO] predictor: combos: {'win': 3, '2t': 26, '3t': 120}
2026-06-10 11:39:27,625 [INFO] run_cycle: fetched 11/4 [scan]: 149 combos
2026-06-10 11:39:27,740 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 66
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 66
  }
]
```

## Phase別通知記録 (24h)
{'final': 27, 'result': 17, 'scan': 22}

## アラート件数 (24h・種類別)
```
  CIRCUIT_BREAKER_TRIP: 70
  ANOMALY_SCRAPER_FAILURE_BURST: 51
  CIRCUIT_BREAKER_NO_ACTION: 51
  CALIBRATION_DRIFT: 35
  FINAL_MISSING: 22
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 4
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 34 | 7 | 10,200 | 5,370 | -4,830 | 0.526 |
| S01_NAKAANA1 | 28 | 7 | 5,600 | 3,080 | -2,520 | 0.55 |
| S02_TETSUBAN | 26 | 6 | 5,200 | 1,780 | -3,420 | 0.342 |

## 直近アラート (24h・新しい順)
```
[11:37:06] CIRCUIT_BREAKER_TRIP: {"cost": 10200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 34, "payout": 5370, "roi_7d": 0.526, "sid": "S00"}
[11:37:06] CALIBRATION_DRIFT: {"avg_actual": 0.2273, "avg_pred": 0.4868, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 88, "overconf_pct": 53.3}
[11:35:06] CIRCUIT_BREAKER_TRIP: {"cost": 5600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 28, "payout": 3080, "roi_7d": 0.55, "sid": "S01_NAKAANA1"}
[11:35:06] CALIBRATION_DRIFT: {"avg_actual": 0.2247, "avg_pred": 0.4835, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 89, "overconf_pct": 53.5}
[11:30:43] CALIBRATION_DRIFT: {"avg_actual": 0.2222, "avg_pred": 0.4837, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 90, "overconf_pct": 54.1}
[11:16:06] CIRCUIT_BREAKER_TRIP: {"cost": 5200, "kind": "CIRCUIT_BREAKER_TRIP", "n": 26, "payout": 1780, "roi_7d": 0.342, "sid": "S02_TETSUBAN"}
[11:16:06] CALIBRATION_DRIFT: {"avg_actual": 0.2247, "avg_pred": 0.4845, "bt": "win", "kind": "CALIBRATION_DRIFT", "n": 89, "overconf_pct": 53.6}
[11:02:29] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[11:02:29] CIRCUIT_BREAKER_TRIP: {"cost": 5400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 27, "payout": 1980, "roi_7d": 0.367, "sid": "S02_TETSUBAN"}
[11:02:29] CIRCUIT_BREAKER_TRIP: {"cost": 10500, "kind": "CIRCUIT_BREAKER_TRIP", "n": 35, "payout": 5370, "roi_7d": 0.511, "sid": "S00"}
```

## 本日残レース: 112件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 32件 締切済
- 通知発射: scan=2 nid / final=2 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- ✅ scan後final無しのまま締切: 0件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 132R | win | 1 | 0.4111 | 2.5 | 1.03 | 200 | scan=2.8 drift=-10.7% | 10:59:20 |
| S02_TETSUBAN | 0711R | win | 1 | 0.5735 | 2.7 | 1.55 | 200 | scan=2.9 drift=-6.9% | 20:13:22 |
| S02_TETSUBAN | 078R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 18:52:32 |
| S02_TETSUBAN | 075R | win | 1 | 0.5476 | 2.0 | 1.10 | 200 | scan=2.1 drift=-4.8% | 17:34:21 |
| S01_NAKAANA1 | 155R | win | 1 | 0.5334 | 4.2 | 2.24 | 200 | scan=- drift=- | 17:21:31 |
| S00 | 074R | win | 1 | 0.5476 | 7.6 | 4.16 | 300 | scan=- drift=- | 17:10:24 |
| S00 | 073R | win | 1 | 0.4111 | 7.5 | 3.08 | 300 | scan=5.2 drift=+44.2% | 16:38:21 |
| S01_NAKAANA1 | 0510R | win | 1 | 0.5123 | 4.1 | 2.10 | 200 | scan=4.5 drift=-8.9% | 16:12:23 |
| S00 | 0510R | win | 1 | 0.5123 | 4.1 | 2.10 | 300 | scan=4.5 drift=-8.9% | 16:12:22 |
| S00 | 0910R | win | 1 | 0.5891 | 8.2 | 4.83 | 300 | scan=- drift=- | 15:10:25 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 46 | +10.8% | -62.9% | +274.6% | 14 | 6 | 26 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 538.5s |
| **Latency** (scan→final max) | 615.1s |
| **Traffic** (notifications 24h) | 66 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S02_TETSUBAN) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 376 | 0.4680 | 0.2952 | +0.1728 | 🟡+37% | 0.2368 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 152 | 0.4194 | 0.2566 | 0.2182 | 🔴-0.14 | 0.786 |
| S01_NAKAANA1 | win | 141 | 0.4875 | 0.2837 | 0.2424 | 🔴-0.19 | 0.706 |
| S02_TETSUBAN | win | 83 | 0.5241 | 0.3855 | 0.2616 | 🔴-0.10 | 0.657 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1254 | 0.1667 | ✅-0.0412 |
| 0.15-0.20 | 5 | 0.1918 | 0.2000 | ✅-0.0082 |
| 0.20-0.30 | 6 | 0.2216 | 0.3333 | 🔴-0.1117 |
| 0.30-0.50 | 144 | 0.4202 | 0.2292 | 🔴+0.1910 |
| 0.50+ | 207 | 0.5410 | 0.3575 | 🔴+0.1835 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 35 | 0.736 |
| win | <5.0 | ✅learned | 65 | 0.727 |
| win | <10.0 | ✅learned | 42 | 0.51 |
| win | <20.0 | ✅learned | 13 | 0.212 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-06-10T11:40:01.789049+09:00_